---
name: forge-agent
description: Brief, build, and prove a new agent (Claude Code subagent/skill, Cursor agent, Agent SDK, Python/LangGraph, scheduled job) before it ships. Use when the user types /forge-agent, says "create/build/design/spec/scaffold an agent", "brief an agent", "ask me the agent questions", or gives a one-liner naming a stack ("SDK + SQLite to do X") but no outcome or eval.
argument-hint: "One-line idea of the agent, however rough"
---

Works well by voice: ask **at most 4 numbered questions per round**, each with a **default**, so
replies like "default" or "1 default, 2 is …" work. One round per message, then wait. Pre-fill whatever
the ask already answers and mark it "taken". If a name or number looks odd (dictation garbles them),
ask ONE question and never guess. Outcome before stack: park any named tech ("Noted SQLite, deciding
at step 3"). Choose the model only after the golden cases exist.

**Config:** `AGENTS_ROOT` is where your agents live (default: `./agents`). `CONSTITUTION` is your rules
file (default: [Constitution of Agents](https://github.com/mjha-arya/constitution-of-agents) `AGENTS.md`)
and `GLOSSARY` is its agent registry.

## Gate 1: Brief (no build without it)
1. **Reuse:** read `GLOSSARY`. If an agent already covers the job, propose extending it instead.
   Report in one line how many agents are still `Authored, not verified` (grep `**Status:**` in
   `AGENTS_ROOT/**/README.md`).
2. **Job** (outcome, not stack) · **Done when** (a number; *default: at least 4/5 golden pass, zero
   safety violations*) · **5 golden cases**, each input → ideal output, at least 1 edge case and at least
   1 adversarial (*default: you draft, the user corrects*).
3. **Data** in → out, with exact paths · what goes stale (*default: re-fetch each run, cache at most 24 h*) ·
   **persist?** If nothing needs to persist, no DB (*default: stdlib `sqlite3`*) · memory write-back.
   Procedural changes go to `PROPOSALS.md` for the user's yes.
4. **Tools:** read set, write = exact paths only, and outward actions (post/email/schedule/deploy) need
   the user's yes · PII/secret check on output · who owns it when it breaks (*default: the user, via
   their notification channel*).
5. **Runtime + REAL auth:** `claude -p` | subagent/skill | Agent SDK | LangGraph. **Test the auth now.**
   Placeholder keys are the most common reason an agent never runs. Single agent or a pattern ·
   `max_turns` · $/run (*default: `claude -p` or subagent, single, 30 turns, $1*).
6. **Failure → behaviour:** login wall, empty data, rate limit, tool error, low confidence
   (*default: retry at most 3 times, exit 2, send a notification, JSONL trace in `data/runs/`*).
→ Write `AGENTS_ROOT/<Name>/BRIEF.md` + `evals/golden.jsonl`. Read it back in 10 lines or fewer and get
  the user's yes. No golden cases → mark it `DRAFT: no eval` and stop.

## Gate 2: Build
7. Read `CONSTITUTION` in full and pick the runtime by its rules (one line).
8. The soul **embeds** the applicable rules (standalone, no links): purpose, inputs, hard rules, a
   `needs_human` list, and an exact return format ending in NOT CHECKED.
9. Build it yourself, or hand large builds to another coding agent with the brief path + spec, then
   review the diff.

## Gate 3: Prove
10. Run **every** golden case on the real model/runtime. Log each to `data/runs/*.jsonl`.
11. Score: deterministic checks + tool-call count (no loops, no duplicate calls) + an LLM judge only
    for the fuzzy part.
12. Fail → fix the soul → commit `"failure fixed → expected change"` → rerun. At most 3 loops, then
    report the blocker honestly.
13. Pass bar met → README `**Status:** Verified (<date>, <score>)`. Otherwise `Authored, not verified`.
    Never claim a run that didn't happen.

## Close
14. Add or update the agent's row in `GLOSSARY` and commit it.
15. Reply in one line: path · score · NOT CHECKED.
