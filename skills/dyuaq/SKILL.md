---
name: dyuaq
description: Do You Understand / Ask Questions. Read the request back as a precise brief, ask only the questions that would change the output, then build it to a stated bar. Use when the user types /dyuaq, or asks you to confirm your understanding, check the ask before building, or "ask me questions first".
argument-hint: "The request, however tangled"
disable-model-invocation: true
---

**DYUAQ — "Do You Understand? / Ask Questions."**

The user has given you something big enough that building the wrong thing is expensive.
Three phases, in order: **mirror**, **ask**, **build**. Do not skip ahead, and do not
collapse them into a single wall of text.

The point is not to be careful-looking. It is to surface the two failure modes that ruin
large tasks — *a wrong reading held silently* and *an assumption never stated* — while they
still cost one message instead of one afternoon.

---

## Phase 1 — Mirror

**Investigate first.** Read the files, run the commands, check the paths. Every question you
could have answered yourself is the expensive kind — it costs a round trip and tells the user
you did not look. Arrive at Phase 2 having already resolved everything resolvable.

**Decompose.** A complex request is almost never one deliverable. A sentence with "and", a
"but", or a trailing "also can you" is two or three asks. Number them. An ask you drop here
is an ask you will not deliver.

Then output the brief — this exact shape, under ~150 words:

> **Deliverable** — what artifact(s), what format, where they land. Numbered if more than one.
> **For** — who reads or uses it, and what they do next with it.
> **Done when** — the concrete test that decides this is finished.
> **I'm assuming** — 2–5 assumptions you will actually act on.
> **Unresolved** — only what genuinely forks the work. Often empty. Empty is a good sign.

**Do not paraphrase their words back.** A mirror that echoes the request is worthless. The
value is entirely in the parts they did not say: the format, the audience, the bar, and the
assumptions you are about to build on.

If you think the request is wrong — wrong tool, wrong shape, a trap downstream — say so here
in one or two sentences. Then build what they asked unless they change it.

---

## Phase 2 — Ask

Use **AskUserQuestion**. Put the brief in your message text, then call the tool in the same
turn — they should read your understanding and answer in one pass.

**The test for whether a question survives:**

> If every option leads to the same work, delete the question.

Also delete:

| Delete a question when… | Do this instead |
|---|---|
| A file, command, or the repo could answer it | Go and look |
| One option is the obvious convention | State it under *I'm assuming* |
| It is reversible in seconds | Pick one, mention it in one clause |
| It is about taste and you can judge it | Decide, and flag it on delivery |
| You are asking permission to do the task | Do the task |

Ask **at most 4** (the tool's limit — treat it as a budget, not a target). One or two is the
common right answer. Zero is correct more often than people think: say *"No blocking
questions — building on the brief above"* and start.

For each question that survives: recommended option **first**, labelled `(Recommended)`, and
one line per option saying what changes if it is chosen. Options must be genuinely different
work, not synonyms.

**One round only.** Ask again only if an answer opened a fork that could not have existed
before. A second round of questions on the same material means Phase 1 was lazy.

---

## Phase 3 — Build

1. **Lock it in one line.** *"Building: \_\_\_, for \_\_\_, done when \_\_\_."* Then stop
   talking about the plan.
2. **Do all of it.** Every numbered item. A partial delivery presented as complete is the
   worst outcome this skill exists to prevent.
3. **Verify, do not assert.** Run the thing. Render the file and look at it. Read the output
   back. "Should work" is not a result — if you did not check it, say the word *unverified*.
4. **Self-check against *Done when*** before you deliver. If it fails your own test, fix it
   first; you set that bar one message ago.
5. **Close with the ledger** — short:
   - what was built, and where it is
   - what you **verified** vs what you **assumed**
   - anything you deliberately left out, and why

If part of the work turns out to be blocked, finish everything else in full and say plainly
what is missing. Scaling the job down is the user's decision, not yours.

---

## Rules

- **Proportionality.** If the request is already unambiguous, do not perform the ceremony.
  Say *"Clear enough — skipping straight to it"* and build. This skill is for tangled asks.
- **Never ask and assume the same thing.** If it is in *I'm assuming*, do not also ask it.
- **The brief is a contract.** Once the user answers, that is the scope. Do not quietly widen
  it because something adjacent looked interesting, and do not narrow it because something
  turned out to be hard.
- **Uncertainty found mid-build** does not restart the cycle. Do everything that does not
  depend on it, then raise the one question at the point it actually blocks you.
- **State the correction, not the apology.** If you discover Phase 1 was wrong, say what
  changed in one sentence and carry on.

## Worked shape

> **Deliverable** — (1) a 2-page PDF summary, (2) the HTML source, both in `./portfolio/`.
> **For** — a prospective client who has 60 seconds before a call.
> **Done when** — it prints clean on A4 and every claim traces to a file in this repo.
> **I'm assuming** — your existing dark theme is for screen, so print gets a light one; no
> client names, since these are external.
> **Unresolved** — one question below.

…then one question, then build.

## Escape hatch

If the ask turns out to be small, or the user just wants an answer, drop the ceremony —
answer directly, or use `/tight` for the compressed version. Reaching for `/dyuaq` on a
one-liner wastes the user's turn, which is the exact cost this skill is meant to save.
