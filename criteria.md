# Acceptance criteria — Provenance Guard

Five criteria that say what "working" means for this service, written in unit 7
**before** you built it.

**All five are yours.** None are given.

An acceptance criterion names a number or something plainly observable. *"The
detector is accurate"* is an opinion — and perfect AI detection isn't possible
anyway, so it's an opinion about something nobody can deliver. *"Of 10 pieces I
wrote myself, at most 1 is labelled high-confidence AI"* is a criterion.

Under each, write a sentence or two on **why that target**. *"I allow at most 1
false positive in 10 because on a writing site a wrong accusation costs more
than a missed detection"* is a real answer.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

**Cover at least three of these five areas.** They're prompts, not a form.

| Area | A question it could answer |
|---|---|
| False positives | How often may a human's writing get called AI? |
| Score spread | How far apart should clearly-AI and clearly-human text score? |
| Label coverage | Is every one of your three labels actually reachable? |
| The appeal path | Does an appeal always change status and always get recorded? |
| Bad input | What happens when `text` is missing, empty, or enormous? |

Two things worth knowing before you pick numbers:

- **The expensive mistake is one-sided.** Missing some AI text costs the site a
  little. Accusing a real writer costs that person a lot. A criterion that
  treats both errors as equally bad is describing a system nobody would ship.
- **Unit 8 tests across three trials, and the target has to hold across all
  three.** Your first signal runs a model, so identical input can score
  differently twice. A target of "at most 1 in 10" against trials of 2, 1, 2 is
  a **miss**.

---
## 1. False positives

Of 10 pieces of text I wrote myself (varied topic and style), at most 1 is labeled high-confidence AI.

**Why this target:** A wrong accusation certainly doubts a real person's integrity, while a missed detection (a false negative) isn't a big deal when it's just a post getting through. Those two costs aren't equal, so the target for the expensive error is strict — 1 in 10, not something looser.

---

## 2. Score spread

Clearly-AI-generated text (raw GPT-2 output, no editing) averages at least 0.30 higher on the combined score than clearly-human text I wrote myself, across the same topic.

**Why this target:** If the two kinds of text land close together, the system isn't measuring anything real — it's just noise with extra steps. 0.30 is roughly the width of the "unsure" band itself, so clearing it means the system is doing more than defaulting to "unsure" on everything.

---

## 3. Label coverage

All three labels — high-confidence human, unsure, high-confidence AI — are each produced by at least one real test submission, not just shown to be reachable by the threshold math.

**Why this target:** A label that only exists on paper is a bug waiting to be found by whoever reads the code next, and unit 8's attack set will find it before I do if I don't check it myself now.

---

## 4. The appeal path

10 out of 10 test appeals against real content_ids change that item's status to `under_review` and show up in `GET /log` immediately afterward.

**Why this target:** There's no prediction happening during this path — no model, no uncertainty, just a lookup and a log write. Unlike the detection scores, nothing here is reasonably allowed to be probabilistic, so it should reasonably be 10/10, not a tolerance.

---

## 5. Bad input

Missing `text` or `creator_id` returns a 400 with a clear error message in 100% of cases; a 50,000-character submission is scored (or cleanly rejected) without crashing the service, in 3 out of 3 tries.

**Why this target:** A crash on bad input doesn't just fail one request — it can take down the service for every writer behind it in the queue. That's a worse failure than a wrong guess, so it gets a zero-tolerance target instead of a rate.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 8 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Uncertain cases land in the unsure band

         The system handles uncertain cases well.

         **Why this target:** ...

         > **Revised in unit 8:** Text I judged borderline scores between
         > 0.4 and 0.6 in at least 4 of 5 cases.
         >
         > **Why revised:** "well" gave me nothing to check. I couldn't
         > reach a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "At most 1 of 10 of my own pieces flagged as AI" → "at most 3
            of 10", because 1 of 10 turned out to be hard.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
