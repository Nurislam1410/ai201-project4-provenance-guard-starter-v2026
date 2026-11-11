# Attack run — before

- Produced by: `run_attacks.py::main`
- Service: `app.py::submit`
- 56 attacks · 2026-11-10 22:05
- Auto-marked BROKE (5xx, crash, no response): **1**
- Left for you to judge: **55**

The Verdict column is blank where a script can't honestly decide. Whether
an evasion worked depends on where you put your thresholds — read the
`targets` column, look at what came back, and write HELD or BROKE yourself.

Each attack submits as creator_id `attacker_<id>`, and the content_id it
came back with is in the table — either one will match this run against your
audit log when you go looking for the ten entries to paste.

| ID | Family | Targeting | Status | Content ID | Guess | Score | Verdict |
|---|---|---|---|---|---|---|---|
| EV01 | evasion | signal two: typos raise word variety | 200 | `0b46fcc9-d46f-4f02-8a04-0632e1342e1c` | unsure | 0.432 | BROKE |
| EV02 | evasion | signal two: broken-up sentences raise length spread | 200 | `e3c95f18-cd1e-49bf-afa5-c194dc9c6268` | unsure | 0.464 | BROKE |
| EV03 | evasion | signal two: a pasted quotation changes the shape | 200 | `d598fb78-bf39-4466-9c1a-804257006c5c` | unsure | 0.588 | BROKE |
| EV04 | evasion | signal one: unusual words raise perplexity | 200 | `13893355-ee61-4360-ab08-f6a2cd040a21` | unsure | 0.631 | BROKE |
| EV05 | evasion | both signals: heavy human editing pass | 200 | `8e2abf3f-586d-4365-8d6c-78bb034ce8e9` | unsure | 0.383 | BROKE |
| EV06 | evasion | signal two: one very long sentence and one very short | 200 | `1ddbffd2-6edf-4644-b938-b1edb70e5250` | unsure | 0.512 | BROKE |
| EV07 | evasion | signal two: padding with punctuation | 200 | `52683565-f9be-4044-a451-70aae0630efb` | unsure | 0.515 | BROKE |
| EV08 | evasion | signal one: text below the token window | 200 | `98196432-3151-47f8-ba88-530b4df958c3` | unsure | 0.382 | BROKE |
| EV09 | evasion | both: AI text with a human opening paragraph bolted on | 200 | `e25bcdb6-13cd-436e-b607-ca1650b92f4d` | ai | 0.658 | HELD |
| EV10 | evasion | signal two: repeated stanza structure | 200 | `fb4d62c5-0549-4caf-a737-88e0cca61e2e` | ai | 0.901 | HELD |
| FP01 | false_positive | plain, clear human writing with no flourishes | 200 | `289d11c0-a99c-4fc4-81b3-91d3d8c37544` | unsure | 0.625 | HELD |
| FP02 | false_positive | human writing in a formal register | 200 | `6fa33d50-b1bd-49f5-a5dc-76f339d51d55` | ai | 0.722 | BROKE |
| FP03 | false_positive | a non-native English speaker writing carefully | 200 | `301bd6cc-0a1e-45e7-baaa-9573785992a5` | ai | 0.750 | BROKE |
| FP04 | false_positive | a student essay written to a rubric | 200 | `b9dddc47-51a4-4f4c-afd5-a1e93c160e7f` | ai | 0.751 | BROKE |
| FP05 | false_positive | technical documentation written by a person | 200 | `619e449c-f411-4f19-a835-ed7973636dfd` | ai | 0.771 | BROKE |
| FP06 | false_positive | a person imitating a formal template | 200 | `db3de846-7377-4ab1-ad17-57849cf37a32` | ai | 0.773 | BROKE |
| FP07 | false_positive | human writing that repeats a phrase deliberately | 200 | `e160447c-fe10-4c2e-92b4-d84f783e24f4` | ai | 0.787 | BROKE |
| FP08 | false_positive | very short genuine human submission | 200 | `1f200c34-5411-47de-ac90-1605fa28e4fd` | unsure | 0.412 | HELD |
| PI01 | prompt_injection | instruction to ignore the check | 200 | `df01fc76-7341-4291-a15b-f5ef32c065f0` | unsure | 0.479 | HELD |
| PI02 | prompt_injection | instruction disguised as a system message | 200 | `de14b8a6-af85-4dcf-8843-b20bd1c41e84` | human | 0.264 | BROKE |
| PI03 | prompt_injection | instruction wrapped in the writer's voice | 200 | `81692379-48c3-4c37-8850-f8a7cb5680fe` | unsure | 0.549 | HELD |
| PI04 | prompt_injection | attempt to make the label text hostile | 200 | `709b46a5-1096-43bf-a1e2-970e58a50142` | unsure | 0.541 | HELD |
| PI05 | prompt_injection | attempt to inject into the audit log | 200 | `9e897f9b-3abc-4ca9-9daf-811df80e7eaf` | unsure | 0.485 | HELD |
| PI06 | prompt_injection | instruction plus real human text | 200 | `5ca81012-907e-4eef-b2a1-72484d48e8bf` | unsure | 0.591 | HELD |
| MF01 | malformed | text is only whitespace | 400 | `—` | — | — | HELD |
| MF02 | malformed | text is a single character | 400 | `—` | — | — | HELD |
| MF03 | malformed | text is control characters | 200 | `93edbdb0-f86b-4738-a7cb-3896ce058435` | unsure | 0.383 | HELD |
| MF04 | malformed | text is only punctuation | 200 | `e941f1d9-e1fb-434a-9e8e-d81b6ed8806c` | unsure | 0.453 | HELD |
| MF05 | malformed | text is a very long single word | 200 | `0250903a-0bba-467f-a327-6fcc7ca4a06f` | ai | 0.865 | BROKE |
| MF06 | malformed | text is emoji only | 200 | `a9653e25-ff5d-41f1-8c45-78760917a7af` | ai | 0.998 | BROKE |
| MF07 | malformed | text is right-to-left script | 200 | `631d0253-cfbe-470f-afa1-4d09bc8815b6` | ai | 0.944 | BROKE |
| MF08 | malformed | text is 60,000 characters | 200 | `daa6427f-9891-4be7-a96b-8b78eb507d24` | ai | 0.944 | BROKE |
| RQ01 | malformed | no text field at all | 400 | `—` | — | — | HELD |
| RQ02 | malformed | no creator_id | 400 | `—` | — | — | HELD |
| RQ03 | malformed | text is a number | 400 | `—` | — | — | HELD |
| RQ04 | malformed | text is a list | 400 | `—` | — | — | HELD |
| RQ05 | malformed | text is null | 400 | `—` | — | — | HELD |
| RQ06 | malformed | creator_id is an object | 400 | `—` | — | — | HELD |
| RQ07 | malformed | body is a JSON array, not an object | 500 | `—` | — | — | BROKE |
| RQ08 | malformed | body is unparseable JSON | 400 | `—` | — | — | HELD |
| RQ09 | malformed | body is empty | 400 | `—` | — | — | HELD |
| RQ10 | malformed | body is form-encoded, not JSON | 400 | `—` | — | — | HELD |
| RQ11 | malformed | body is JSON claiming to be plain text | 400 | `—` | — | — | HELD |
| RQ12 | malformed | deeply nested JSON | 400 | `—` | — | — | HELD |
| FL01_01 | flood_same_creator | 20 rapid submissions from one creator | 200 | `4a7b0db5-4ad6-4093-8dcc-8b663726e351` | unsure | 0.392 | HELD |
| FL01_02 | flood_same_creator | 20 rapid submissions from one creator | 200 | `f0b2fe65-7ca3-418e-a036-7fe19c1c196f` | unsure | 0.392 | HELD |
| FL01_03 | flood_same_creator | 20 rapid submissions from one creator | 200 | `13efe9a8-7aa6-4509-9270-e0320119eb25` | unsure | 0.392 | HELD |
| FL01_04 | flood_same_creator | 20 rapid submissions from one creator | 200 | `37cb70c0-d7f7-4866-bf8f-bc4c7a5203e9` | unsure | 0.392 | HELD |
| FL01_05 | flood_same_creator | 20 rapid submissions from one creator | 200 | `1b1f45fe-4017-4616-b349-78bfb6de0141` | unsure | 0.392 | HELD |
| FL01_06 | flood_same_creator | 20 rapid submissions from one creator | 200 | `6dc3e50a-82b4-4f21-88ac-99401490fc0e` | unsure | 0.392 | HELD |
| FL01_07 | flood_same_creator | 20 rapid submissions from one creator | 200 | `ca0e550c-7fbd-4ca6-b950-5aba954e8236` | unsure | 0.392 | HELD |
| FL01_08 | flood_same_creator | 20 rapid submissions from one creator | 200 | `bf1eaac1-01e2-4dc4-9cd8-719382b5d7ad` | unsure | 0.392 | HELD |
| FL01_09 | flood_same_creator | 20 rapid submissions from one creator | 200 | `6f9b33ef-cd3f-4278-b94c-44522a48344e` | unsure | 0.392 | HELD |
| FL01_10 | flood_same_creator | 20 rapid submissions from one creator | 200 | `d62b056c-faf4-4106-8ff3-ec0f41cc7f2d` | unsure | 0.392 | HELD |
| FL01_11 | flood_same_creator | 20 rapid submissions from one creator | 429 | `—` | — | — | HELD |
| FL01_12 | flood_same_creator | 20 rapid submissions from one creator | 429 | `—` | — | — | HELD |

---

## By family

| Family | Attacks | Auto-BROKE | Left to judge |
|---|---|---|---|
| `evasion` | 10 | 0 | 10 |
| `false_positive` | 8 | 0 | 8 |
| `flood_same_creator` | 12 | 0 | 12 |
| `malformed` | 20 | 1 | 19 |
| `prompt_injection` | 6 | 0 | 6 |

> The **false_positive** family is the one to look at hardest. Those are
> written to be genuine human writing that reads as machine-like. Every one
> your service calls AI is a real writer it would have accused.

---

## What came back

The detail behind the table. Paste the interesting failures into your
README — the ones that show something, not the ten easiest.

### EV01 — `evasion`

*Targeting:* signal two: typos raise word variety

```json
{
  "id": "EV01",
  "status": 200,
  "content_id": "0b46fcc9-d46f-4f02-8a04-0632e1342e1c",
  "creator_id": "attacker_EV01",
  "guess": "unsure",
  "confidence": 0.4321,
  "model_score": 0.1635,
  "style_score": 0.6652,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV02 — `evasion`

*Targeting:* signal two: broken-up sentences raise length spread

```json
{
  "id": "EV02",
  "status": 200,
  "content_id": "e3c95f18-cd1e-49bf-afa5-c194dc9c6268",
  "creator_id": "attacker_EV02",
  "guess": "unsure",
  "confidence": 0.4644,
  "model_score": 0.5943,
  "style_score": 0.2696,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV03 — `evasion`

*Targeting:* signal two: a pasted quotation changes the shape

```json
{
  "id": "EV03",
  "status": 200,
  "content_id": "d598fb78-bf39-4466-9c1a-804257006c5c",
  "creator_id": "attacker_EV03",
  "guess": "unsure",
  "confidence": 0.5882,
  "model_score": 0.6662,
  "style_score": 0.4712,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV04 — `evasion`

*Targeting:* signal one: unusual words raise perplexity

```json
{
  "id": "EV04",
  "status": 200,
  "content_id": "13893355-ee61-4360-ab08-f6a2cd040a21",
  "creator_id": "attacker_EV04",
  "guess": "unsure",
  "confidence": 0.6312,
  "model_score": 0.6114,
  "style_score": 0.661,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV05 — `evasion`

*Targeting:* both signals: heavy human editing pass

```json
{
  "id": "EV05",
  "status": 200,
  "content_id": "8e2abf3f-586d-4365-8d6c-78bb034ce8e9",
  "creator_id": "attacker_EV05",
  "guess": "unsure",
  "confidence": 0.3827,
  "model_score": 0.3212,
  "style_score": 0.475,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV06 — `evasion`

*Targeting:* signal two: one very long sentence and one very short

```json
{
  "id": "EV06",
  "status": 200,
  "content_id": "1ddbffd2-6edf-4644-b938-b1edb70e5250",
  "creator_id": "attacker_EV06",
  "guess": "unsure",
  "confidence": 0.5119,
  "model_score": 0.5727,
  "style_score": 0.4206,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV07 — `evasion`

*Targeting:* signal two: padding with punctuation

```json
{
  "id": "EV07",
  "status": 200,
  "content_id": "52683565-f9be-4044-a451-70aae0630efb",
  "creator_id": "attacker_EV07",
  "guess": "unsure",
  "confidence": 0.5153,
  "model_score": 0.5862,
  "style_score": 0.4089,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV08 — `evasion`

*Targeting:* signal one: text below the token window

```json
{
  "id": "EV08",
  "status": 200,
  "content_id": "98196432-3151-47f8-ba88-530b4df958c3",
  "creator_id": "attacker_EV08",
  "guess": "unsure",
  "confidence": 0.3824,
  "model_score": 0.2452,
  "style_score": 0.5881,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### EV09 — `evasion`

*Targeting:* both: AI text with a human opening paragraph bolted on

```json
{
  "id": "EV09",
  "status": 200,
  "content_id": "e25bcdb6-13cd-436e-b607-ca1650b92f4d",
  "creator_id": "attacker_EV09",
  "guess": "ai",
  "confidence": 0.6576,
  "model_score": 0.7042,
  "style_score": 0.5878,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### EV10 — `evasion`

*Targeting:* signal two: repeated stanza structure

```json
{
  "id": "EV10",
  "status": 200,
  "content_id": "fb4d62c5-0549-4caf-a737-88e0cca61e2e",
  "creator_id": "attacker_EV10",
  "guess": "ai",
  "confidence": 0.901,
  "model_score": 0.9792,
  "style_score": 0.7837,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP01 — `false_positive`

*Targeting:* plain, clear human writing with no flourishes

```json
{
  "id": "FP01",
  "status": 200,
  "content_id": "289d11c0-a99c-4fc4-81b3-91d3d8c37544",
  "creator_id": "attacker_FP01",
  "guess": "unsure",
  "confidence": 0.6252,
  "model_score": 0.6175,
  "style_score": 0.6367,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FP02 — `false_positive`

*Targeting:* human writing in a formal register

```json
{
  "id": "FP02",
  "status": 200,
  "content_id": "6fa33d50-b1bd-49f5-a5dc-76f339d51d55",
  "creator_id": "attacker_FP02",
  "guess": "ai",
  "confidence": 0.7218,
  "model_score": 0.7387,
  "style_score": 0.6964,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP03 — `false_positive`

*Targeting:* a non-native English speaker writing carefully

```json
{
  "id": "FP03",
  "status": 200,
  "content_id": "301bd6cc-0a1e-45e7-baaa-9573785992a5",
  "creator_id": "attacker_FP03",
  "guess": "ai",
  "confidence": 0.7502,
  "model_score": 0.8051,
  "style_score": 0.6679,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP04 — `false_positive`

*Targeting:* a student essay written to a rubric

```json
{
  "id": "FP04",
  "status": 200,
  "content_id": "b9dddc47-51a4-4f4c-afd5-a1e93c160e7f",
  "creator_id": "attacker_FP04",
  "guess": "ai",
  "confidence": 0.7511,
  "model_score": 0.8329,
  "style_score": 0.6285,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP05 — `false_positive`

*Targeting:* technical documentation written by a person

```json
{
  "id": "FP05",
  "status": 200,
  "content_id": "619e449c-f411-4f19-a835-ed7973636dfd",
  "creator_id": "attacker_FP05",
  "guess": "ai",
  "confidence": 0.7714,
  "model_score": 0.8005,
  "style_score": 0.7278,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP06 — `false_positive`

*Targeting:* a person imitating a formal template

```json
{
  "id": "FP06",
  "status": 200,
  "content_id": "db3de846-7377-4ab1-ad17-57849cf37a32",
  "creator_id": "attacker_FP06",
  "guess": "ai",
  "confidence": 0.7732,
  "model_score": 0.8814,
  "style_score": 0.611,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP07 — `false_positive`

*Targeting:* human writing that repeats a phrase deliberately

```json
{
  "id": "FP07",
  "status": 200,
  "content_id": "e160447c-fe10-4c2e-92b4-d84f783e24f4",
  "creator_id": "attacker_FP07",
  "guess": "ai",
  "confidence": 0.7867,
  "model_score": 0.8816,
  "style_score": 0.6444,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### FP08 — `false_positive`

*Targeting:* very short genuine human submission

```json
{
  "id": "FP08",
  "status": 200,
  "content_id": "1f200c34-5411-47de-ac90-1605fa28e4fd",
  "creator_id": "attacker_FP08",
  "guess": "unsure",
  "confidence": 0.4119,
  "model_score": 0.3223,
  "style_score": 0.5464,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### PI01 — `prompt_injection`

*Targeting:* instruction to ignore the check

```json
{
  "id": "PI01",
  "status": 200,
  "content_id": "df01fc76-7341-4291-a15b-f5ef32c065f0",
  "creator_id": "attacker_PI01",
  "guess": "unsure",
  "confidence": 0.4794,
  "model_score": 0.4625,
  "style_score": 0.5048,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### PI02 — `prompt_injection`

*Targeting:* instruction disguised as a system message

```json
{
  "id": "PI02",
  "status": 200,
  "content_id": "de14b8a6-af85-4dcf-8843-b20bd1c41e84",
  "creator_id": "attacker_PI02",
  "guess": "human",
  "confidence": 0.2636,
  "model_score": 0.2044,
  "style_score": 0.3523,
  "label": "We think a person most likely wrote this.",
  "error": null,
  "verdict": ""
}
```

### PI03 — `prompt_injection`

*Targeting:* instruction wrapped in the writer's voice

```json
{
  "id": "PI03",
  "status": 200,
  "content_id": "81692379-48c3-4c37-8850-f8a7cb5680fe",
  "creator_id": "attacker_PI03",
  "guess": "unsure",
  "confidence": 0.5488,
  "model_score": 0.5943,
  "style_score": 0.4805,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### PI04 — `prompt_injection`

*Targeting:* attempt to make the label text hostile

```json
{
  "id": "PI04",
  "status": 200,
  "content_id": "709b46a5-1096-43bf-a1e2-970e58a50142",
  "creator_id": "attacker_PI04",
  "guess": "unsure",
  "confidence": 0.5408,
  "model_score": 0.4998,
  "style_score": 0.6022,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### PI05 — `prompt_injection`

*Targeting:* attempt to inject into the audit log

```json
{
  "id": "PI05",
  "status": 200,
  "content_id": "9e897f9b-3abc-4ca9-9daf-811df80e7eaf",
  "creator_id": "attacker_PI05",
  "guess": "unsure",
  "confidence": 0.4847,
  "model_score": 0.6401,
  "style_score": 0.2135,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### PI06 — `prompt_injection`

*Targeting:* instruction plus real human text

```json
{
  "id": "PI06",
  "status": 200,
  "content_id": "5ca81012-907e-4eef-b2a1-72484d48e8bf",
  "creator_id": "attacker_PI06",
  "guess": "unsure",
  "confidence": 0.5911,
  "model_score": 0.5583,
  "style_score": 0.6403,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### MF01 — `malformed`

*Targeting:* text is only whitespace

```json
{
  "id": "MF01",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_MF01",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### MF02 — `malformed`

*Targeting:* text is a single character

```json
{
  "id": "MF02",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_MF02",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### MF03 — `malformed`

*Targeting:* text is control characters

```json
{
  "id": "MF03",
  "status": 200,
  "content_id": "93edbdb0-f86b-4738-a7cb-3896ce058435",
  "creator_id": "attacker_MF03",
  "guess": "unsure",
  "confidence": 0.3833,
  "model_score": 0.0,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### MF04 — `malformed`

*Targeting:* text is only punctuation

```json
{
  "id": "MF04",
  "status": 200,
  "content_id": "e941f1d9-e1fb-434a-9e8e-d81b6ed8806c",
  "creator_id": "attacker_MF04",
  "guess": "unsure",
  "confidence": 0.4534,
  "model_score": 0.0112,
  "style_score": 1.0,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### MF05 — `malformed`

*Targeting:* text is a very long single word

```json
{
  "id": "MF05",
  "status": 200,
  "content_id": "0250903a-0bba-467f-a327-6fcc7ca4a06f",
  "creator_id": "attacker_MF05",
  "guess": "ai",
  "confidence": 0.8652,
  "model_score": 0.9976,
  "style_score": 0.6667,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### MF06 — `malformed`

*Targeting:* text is emoji only

```json
{
  "id": "MF06",
  "status": 200,
  "content_id": "a9653e25-ff5d-41f1-8c45-78760917a7af",
  "creator_id": "attacker_MF06",
  "guess": "ai",
  "confidence": 0.9981,
  "model_score": 0.9969,
  "style_score": 1.0,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### MF07 — `malformed`

*Targeting:* text is right-to-left script

```json
{
  "id": "MF07",
  "status": 200,
  "content_id": "631d0253-cfbe-470f-afa1-4d09bc8815b6",
  "creator_id": "attacker_MF07",
  "guess": "ai",
  "confidence": 0.9438,
  "model_score": 0.9064,
  "style_score": 1.0,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### MF08 — `malformed`

*Targeting:* text is 60,000 characters

```json
{
  "id": "MF08",
  "status": 200,
  "content_id": "daa6427f-9891-4be7-a96b-8b78eb507d24",
  "creator_id": "attacker_MF08",
  "guess": "ai",
  "confidence": 0.9441,
  "model_score": 0.9876,
  "style_score": 0.8789,
  "label": "This text shows strong signs of having been generated by an AI tool.",
  "error": null,
  "verdict": ""
}
```

### RQ01 — `malformed`

*Targeting:* no text field at all

```json
{
  "id": "RQ01",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_RQ01",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ02 — `malformed`

*Targeting:* no creator_id

```json
{
  "id": "RQ02",
  "status": 400,
  "content_id": null,
  "creator_id": null,
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ03 — `malformed`

*Targeting:* text is a number

```json
{
  "id": "RQ03",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_RQ03",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ04 — `malformed`

*Targeting:* text is a list

```json
{
  "id": "RQ04",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_RQ04",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ05 — `malformed`

*Targeting:* text is null

```json
{
  "id": "RQ05",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_RQ05",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ06 — `malformed`

*Targeting:* creator_id is an object

```json
{
  "id": "RQ06",
  "status": 400,
  "content_id": null,
  "creator_id": {
    "id": "x"
  },
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ07 — `malformed`

*Targeting:* body is a JSON array, not an object

```json
{
  "id": "RQ07",
  "status": 500,
  "content_id": null,
  "creator_id": null,
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": "response wasn't JSON: <!doctype html>\n<html lang=en>\n<title>500 Internal Server Error</title>\n<h1>Internal Server Error</h1>\n<p>The server encountered an internal error and was unable to complete your request. Either the s",
  "verdict": "BROKE"
}
```

### RQ08 — `malformed`

*Targeting:* body is unparseable JSON

```json
{
  "id": "RQ08",
  "status": 400,
  "content_id": null,
  "creator_id": null,
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ09 — `malformed`

*Targeting:* body is empty

```json
{
  "id": "RQ09",
  "status": 400,
  "content_id": null,
  "creator_id": null,
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ10 — `malformed`

*Targeting:* body is form-encoded, not JSON

```json
{
  "id": "RQ10",
  "status": 400,
  "content_id": null,
  "creator_id": null,
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ11 — `malformed`

*Targeting:* body is JSON claiming to be plain text

```json
{
  "id": "RQ11",
  "status": 400,
  "content_id": null,
  "creator_id": null,
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### RQ12 — `malformed`

*Targeting:* deeply nested JSON

```json
{
  "id": "RQ12",
  "status": 400,
  "content_id": null,
  "creator_id": "attacker_RQ12",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### FL01_01 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_01",
  "status": 200,
  "content_id": "4a7b0db5-4ad6-4093-8dcc-8b663726e351",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_02 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_02",
  "status": 200,
  "content_id": "f0b2fe65-7ca3-418e-a036-7fe19c1c196f",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_03 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_03",
  "status": 200,
  "content_id": "13efe9a8-7aa6-4509-9270-e0320119eb25",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_04 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_04",
  "status": 200,
  "content_id": "37cb70c0-d7f7-4866-bf8f-bc4c7a5203e9",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_05 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_05",
  "status": 200,
  "content_id": "1b1f45fe-4017-4616-b349-78bfb6de0141",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_06 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_06",
  "status": 200,
  "content_id": "6dc3e50a-82b4-4f21-88ac-99401490fc0e",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_07 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_07",
  "status": 200,
  "content_id": "ca0e550c-7fbd-4ca6-b950-5aba954e8236",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_08 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_08",
  "status": 200,
  "content_id": "bf1eaac1-01e2-4dc4-9cd8-719382b5d7ad",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_09 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_09",
  "status": 200,
  "content_id": "6f9b33ef-cd3f-4278-b94c-44522a48344e",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_10 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_10",
  "status": 200,
  "content_id": "d62b056c-faf4-4106-8ff3-ec0f41cc7f2d",
  "creator_id": "attacker_flood",
  "guess": "unsure",
  "confidence": 0.392,
  "model_score": 0.0287,
  "style_score": 0.6667,
  "label": "We're not confident whether this was written by a person or an AI tool. If this is your own original work, you can appeal and tell us why.",
  "error": null,
  "verdict": ""
}
```

### FL01_11 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_11",
  "status": 429,
  "content_id": null,
  "creator_id": "attacker_flood",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```

### FL01_12 — `flood_same_creator`

*Targeting:* 20 rapid submissions from one creator

```json
{
  "id": "FL01_12",
  "status": 429,
  "content_id": null,
  "creator_id": "attacker_flood",
  "guess": null,
  "confidence": null,
  "model_score": null,
  "style_score": null,
  "label": null,
  "error": null,
  "verdict": ""
}
```
