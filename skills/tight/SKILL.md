---
name: tight
description: Decode a complicated, multi-part or ambiguous ask and answer it in under 80 words as bullets or a table. Invoke when the user types /tight, or asks to be answered concisely, tightly, briefly, or "in bullets".
argument-hint: "The question, however messy"
---

The user has a question that is tangled — several asks in one sentence, an unstated
assumption, or a decision hiding inside a request for information. Untangle it, then answer
tight enough to read in one glance.

## Procedure

1. **Decode.** Identify every distinct ask in the message, including the implied one. A
   question phrased as "can we..." is usually a request to do it, not to assess feasibility.
   A question with a "but" in it is usually two questions.
2. **Commit to a reading.** If the ask is ambiguous, pick the most useful interpretation and
   state it in one short line: *"Reading this as: ___."* Never answer two readings in
   parallel, and never open with a clarifying question you could resolve yourself.
3. **Answer.** Under 80 words of prose, excluding code blocks and command output.
4. **Cut, then cut again.** Delete anything that survives only because it is true.

## Format

- Numbered blocks for a multi-part ask, matching the order asked.
- A table when there are 3+ items with 2+ shared attributes. Otherwise bullets.
- Bold the single load-bearing word per bullet — the one that carries the decision.
- One line per bullet. If a bullet needs a second line, it is two bullets or it is filler.

## Rules

- **Recommend, do not survey.** One answer. If alternatives matter, they are a table with a
  "pick this if" column, not paragraphs of even-handedness.
- **Lead with the conclusion.** Reasoning goes after, and only if it changes what to do.
- **Never restate the question**, recap what you just did, or close with a summary.
- **Say the uncomfortable part in the fewest words**, rather than softening it into length.
- **At most one question at the end**, and only when the answer changes the next action.
- Verify before asserting. Brevity is not licence to guess — an unchecked claim stated
  tersely is worse than a long hedge. Say "unverified" in one word and move on.

## Escape hatch

If the honest answer genuinely does not compress — a real design trade-off, a plan with
dependencies, a failure that needs evidence — write the short version first, then offer the
long one in a single line: *"Longer version if useful."* Do not silently exceed the budget.
