# Provenance Guard

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first.**
>
> Once `python test.py` passes, in one terminal:
>
> ```bash
> python app.py
> ```
>
> and in another:
>
> ```bash
> curl -X POST http://127.0.0.1:5000/ping \
>   -H "Content-Type: application/json" \
>   -d '{"message": "hello"}'
> ```
>
> That's a web service. Something sent it text and it sent something back.
> Everything this unit is filling in the middle.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     Unit 7 asks for the first five sections. Unit 8 adds the five below.

     Everything is pasted as TEXT. A pasted curl response gets full credit;
     a picture of your terminal gets none.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 7 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- The path a submission takes, from arriving to the label a reader sees.
     Six or seven steps — this is the trace you wrote in Milestone 1. -->

1. A writer's text and `creator_id` arrive as JSON at `POST /submit`.
2. The route validates the input first — missing or empty `text`/`creator_id` is rejected immediately with a 400, before any scoring happens.
3. The model signal (`detector.model_signal`) runs a small local language model over the text and turns how *predictable* it is into a 0-1 score.
4. The style signal (`stylometry.style_signal`) measures the text's shape — sentence-length spread, vocabulary variety, and expressive punctuation — without reading it for meaning at all.
5. `scoring.combine_signals` blends both into one 0-1 confidence score, pulling the result toward 0.5 if the two signals disagree sharply.
6. `scoring.score_to_label` turns that number into one of three plain-English labels a non-technical reader can understand.
7. The full decision — both signal scores, the combined score, the label, and a fresh `content_id` — is written to the audit log and returned to the caller. If the writer disagrees, `POST /appeal` lets them attach their reasoning, which flips that item's status to `under_review` in the same log.

---

## Signals and Scoring

<!-- For each signal: what property it measures, why that might differ between
     human and AI writing, and WHAT IT CAN'T SEE.

     The blind spot is not optional. If you can't name it you don't understand
     the signal yet — and unit 8's attack set is built out of blind spots. -->

### Signal one — the model signal

**What it measures:** How predictable the text is to a small local language model (GPT-2), turned into a 0-1 score via perplexity. Lower perplexity (more predictable) scores closer to 1 ("more AI-like").

**Why that might differ between human and AI writing:** A language model writes by repeatedly picking a likely next word, so text it produced tends to be text it also finds easy to predict. Human writing wanders more — odd word choices, abrupt turns, the specific rather than the typical.

**What it can't see:** Predictability isn't the same thing as authorship. This signal actually rewards common words in short, ordinary sentences — so someone writing in a second language, a younger writer, or anyone writing plainly on purpose can score as machine-like, while dense, rare-word-heavy prose often scores as *human* just because a model can't predict it. The writers this signal is most likely to accuse are the ones with the least room to argue back.

### Signal two — the style signal

**What it measures:** The text's shape, not its meaning — sentence-length spread (coefficient of variation of words per sentence), vocabulary variety (unique words / total words), and expressive punctuation density (semicolons, colons, em dashes, ellipses, "!", "?" per 100 words). All three are flipped and averaged so the result points the same way as signal one: higher = more AI-like.

**Why that might differ between human and AI writing:** Generated prose tends toward even, mid-length sentences and a narrower vocabulary band, because that's what "most likely next word" produces on average. Human writing is lumpier — a three-word sentence next to a forty-word one, a personal punctuation habit.

**What it can't see:** This signal cannot read. It has no idea what the text says, so anything that changes the shape without changing the substance — added typos, breaking up sentences, a pasted quotation — moves the score. It also shares signal one's blind spot from a different angle: a short, plain, evenly-punctuated human paragraph (a quick note, a simple instruction) scores just as "AI-like" as real AI output, because it's genuinely uniform in shape — plainness gets mistaken for generation either way.

### The combining rule

<!-- Write the rule in words, then give the numbers. What happens when the two
     signals disagree? -->

**The rule:** Weighted average — 0.6 × model signal + 0.4 × style signal. The model signal is trained on language and gets more trust than three hand-picked heuristics. If the two signals disagree by more than 0.4, that disagreement is treated as evidence of uncertainty on its own: the weighted average gets pulled halfway toward 0.5 instead of taken at face value. This widens the unsure band specifically in the disagreement case, which is where a false accusation is most likely to come from one signal overruling a doubtful other.

**The numbers:** `WEIGHT_MODEL_SIGNAL = 0.6`, `WEIGHT_STYLE_SIGNAL = 0.4` (config.py). Disagreement threshold: 0.4. When exceeded, the result moves 50% of the way from the weighted average toward 0.5.

**Where it lives:** `scoring.py::combine_signals`

<!-- ⚠️ The grader checks your code against that line. If your rule lives
     somewhere else, say where. -->

**A case where my two signals split, and what my rule does with it:**

`"The weather is nice today. It's sunny; it's warm. I like it a lot! Don't you? This is good -- really good."` — model_score 0.767 (common, plain words read as predictable/AI-ish to signal one), style_score 0.295 (short, varied sentence lengths and heavy punctuation variety read as human-ish to signal two). Disagreement is 0.472, over the 0.4 threshold, so the rule pulls the weighted average (0.578) halfway toward 0.5, landing at 0.539 — "unsure" instead of a confident "ai" that a plain average would have been closer to. This is exactly the plain-writing blind spot both signals share from different angles, showing up as a split rather than a shared wrong answer.


---

## Label Variants

<!-- The exact text of all three labels, as a reader would see them, and the
     score range each covers.

     Write them for someone who has never heard the word "threshold". -->

| Label | Score range | The exact text a reader sees |
|---|---|---|
| high-confidence human | 0.00 – 0.35 | "We think a person most likely wrote this." |
| unsure | 0.35 – 0.65 | "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why." |
| high-confidence AI | 0.65 – 1.00 | "This text shows strong signs of having been generated by an AI tool." |

**Why I worded the "unsure" one this way:**
<!-- It's the hardest of the three. It has to admit uncertainty without
     sounding like an accusation, because the person reading it may well have
     written every word themselves. -->

It states the uncertainty plainly instead of hedging around it, and it never says anything that implies the writer did something wrong. It also hands them an action — the appeal — in the same sentence, instead of leaving them with only a verdict to sit with. That matters most here specifically because the person reading it may have written every single word themselves.


---

## Sample Run

<!-- One submission and one appeal, pasted as text: the request, the response,
     and the log entries. -->

**A submission**

<!-- The response needs content_id, guess, confidence, label, AND both
     signal scores - model_score and style_score. Unit 8's tools read those
     two off the response, so leaving them out costs you next unit's
     diagnostics. -->

```bash
$ curl -X POST http://127.0.0.1:5000/submit \
  -H "Content-Type: application/json" \
  -d '{"text": "I went to the store today. I bought some milk and bread. Then I walked home. It was a nice day.", "creator_id": "calibration-plain"}'
```

```json
{
  "confidence": 0.7737,
  "content_id": "fb0eb017-d4ec-437a-957b-22225867f305",
  "guess": "ai",
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "model_score": 0.8577,
  "style_score": 0.6478
}
```

**An appeal**

```bash
$ curl -X POST http://127.0.0.1:5000/appeal \
  -H "Content-Type: application/json" \
  -d '{"content_id": "fb0eb017-d4ec-437a-957b-22225867f305", "reasoning": "I wrote this myself, it is just a plain description of my day."}'
```

```json
{
  "content_id": "fb0eb017-d4ec-437a-957b-22225867f305",
  "message": "Appeal recorded. This submission is now under review.",
  "ok": true,
  "status": "under_review"
}
```

**What the log shows afterwards**

```bash
$ curl "http://127.0.0.1:5000/log?limit=10"
# (filtered here to the two entries for this content_id — the original
# decision stays exactly where it was, the appeal sits after it, append-only)
```

```json
[
  {
    "combined_score": 0.7737,
    "content_id": "fb0eb017-d4ec-437a-957b-22225867f305",
    "creator_id": "calibration-plain",
    "guess": "ai",
    "label": "This text shows strong signs of having been generated by an AI tool.",
    "model_score": 0.8577,
    "status": "decided",
    "style_score": 0.6478,
    "timestamp": "2026-11-04T06:26:22+00:00"
  },
  {
    "content_id": "fb0eb017-d4ec-437a-957b-22225867f305",
    "creator_id": "calibration-plain",
    "event": "appeal",
    "reasoning": "I wrote this myself, it is just a plain description of my day.",
    "status": "under_review",
    "timestamp": "2026-11-04T06:46:53+00:00"
  }
]
```

---

## How I Used AI

**Moment 1**

- *What I asked for:* I gave Claude the whole project description up front and asked it to keep scanning that against our progress the whole time we worked, so I wouldn't miss an undone requirement.
- *What came back:* It kept checking our work against the brief's actual requirements as we went — for example, that both signal scores have to be in the `/submit` response, not just the log, and that all three labels have to be reachable, not just mathematically possible.
- *What I changed:* Nothing — this was a standing instruction for how we'd work together, not a one-off prompt.

**Moment 2**

- *What I asked for:* With real time pressure (about 45 minutes left), I asked to split the work: I do all the reasoning, Claude does the rest — the typing, the testing, the execution.
- *What came back:* Claude proposed concrete starting numbers for me to confirm or correct — the stylometry formula, the 0.6/0.4 combine weights, the label thresholds, and five draft criteria numbers. When I asked it to just write the acceptance-criteria reasoning and the AI-use disclosure *for* me to paraphrase as my own, it refused twice and pushed back that this would be misrepresenting authorship rather than delegating execution.
- *What I changed:* I rewrote the "why" line under two of the five criteria (false positives, the appeal path) in my own words after that pushback, instead of keeping Claude's drafted reasoning.

<!-- ═══════════════════════ UNIT 8 — THE TEST ═══════════════════════ -->

---

## Rate Limiting

**My limits:** ___ per minute, ___ per day

**Why those numbers and not others:**
<!-- Think about two people: a real writer submitting their own work a few
     times an hour, and a script sending a thousand variations to map your
     thresholds. Your numbers have to be liveable for the first and hostile to
     the second. -->

**What a caller counts as:** <!-- per address, or per creator_id? They fail
differently — one script can look like a thousand callers, and one household
can look like one. -->

**The run of status codes when I pushed past it:**

<!-- python run_attacks.py --flood 15 -->

```

```

---

## Attack Run — Before

<!-- Every attack with its outcome and a held-or-broke mark.
     `run_attacks.py --label before` produces the table. -->



**Ten audit log entries from the run**

<!-- Choose entries that show the interesting failures, not the ten easiest. -->

```json

```

**The single worst outcome** — the one I'd least want to explain to a writer
whose work got caught by it:



---

## Run Log and Verdicts

<!-- Your five criteria across three trials. `run_eval.py --label before`. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Real output from one trial**, pasted as text, naming the file and function
that produced it:

```json

```

**Diagnoses**

<!-- For each miss AND each broken attack: the stage and the mechanism.

     Your service has five stages: the route, signal one, signal two, the
     combining rule, and the label mapping.

     Not a diagnosis:  "The evasion attacks got through."
     A diagnosis:      "Four evasion inputs got through. All four had typos
                        added to AI-generated text. My second signal measures
                        word variety, and typos raise word variety — so it read
                        them as more human. My combining rule weights that
                        signal at 0.6, so it dragged the whole score down."

     Look for a pattern. Five failures on one signal is one problem, not five. -->



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Attack Run — After

<!-- Same format. `run_attacks.py --label after` -->



**Did it help, and how do I know:**

<!-- Widening the unsure band usually fixes one problem and creates another.
     Reporting that trade honestly is worth full credit. -->



---

## What's Still Broken

<!-- For each attack still getting through and each criterion still missed:
     what you'd do, and why you stopped. -->



**The trade I'd make if this ran for real:**

<!-- Two sentences. Fewer wrong accusations means more AI text getting through.
     Say which way you'd go and WHO PAYS FOR IT. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 7

       [ ] criteria.md has five numbered criteria, each naming a target
       [ ] Each has a reason underneath
       [ ] POST /submit returns content_id, guess, confidence, label,
           model_score and style_score
       [ ] Two signals that measure DIFFERENT things, each with a named blind spot
       [ ] Three label variants, all reachable, written out in full
       [ ] POST /appeal changes status and writes to the log
       [ ] Signals and Scoring names scoring.py::combine_signals
       [ ] Sample Run: a submission AND an appeal, as pasted text
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 8

       [ ] Rate limiting on /submit, with your numbers justified
       [ ] The pasted run of status codes showing 429
       [ ] Audit log with all nine fields, recording rejections too
       [ ] The attack set run IN FULL, every input with an outcome
       [ ] Ten audit log entries pasted as text
       [ ] Five criteria across three trials
       [ ] A diagnosis for every miss and every broken attack — stage AND mechanism
       [ ] One improvement, with Attack Run — After
       [ ] What's Still Broken, including the production trade
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
