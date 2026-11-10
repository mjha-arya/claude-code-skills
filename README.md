# claude-code-skills

> **Skills and subagents that make Claude Code ask better questions, answer tighter, build agents to an evidence bar, and review changes the way a security engineer would.**

Each one is a single Markdown file. Copy it into `~/.claude/skills/<name>/` (skills) or `~/.claude/agents/` (subagents) and it's available in every project.

| | Type | What it does | Invoke |
|---|---|---|---|
| **[dyuaq](skills/dyuaq/SKILL.md)** | skill | *"Do You Understand? / Ask Questions."* For big asks: mirror the request back as a precise brief (deliverable, audience, done-when, assumptions), ask only questions whose answer changes the work, then build and verify against the stated bar | `/dyuaq <request>` |
| **[tight](skills/tight/SKILL.md)** | skill | Untangles a messy multi-part question and answers it in under 80 words. Commits to one reading, recommends instead of surveying, bolds the load-bearing word | `/tight <question>` |
| **[forge-agent](skills/forge-agent/SKILL.md)** | skill | Brief → build → prove a new agent. Golden cases come before the model choice, auth is tested up front, and status is *Verified* only after every golden case runs | `/forge-agent <idea>` |
| **[senior-security](agents/senior-security.md)** | subagent | Reviews a diff, dependency bump or vendor update by **capability delta**: what it can now do that its declared purpose doesn't justify. Review only, never writes exploits | "run the senior security agent" |

## Install

```bash
git clone https://github.com/mjha-arya/claude-code-skills
cp -r claude-code-skills/skills/* ~/.claude/skills/
cp claude-code-skills/agents/*.md ~/.claude/agents/
```

## Why these exist

They encode three habits that separate agent work that ships from agent work that demos:

1. **Understand before building.** Most expensive failures are a wrong reading held silently (`dyuaq`).
2. **Evidence, not assertion.** "Done" means verified against a bar set in advance (`forge-agent`).
3. **Least privilege.** Ask what changed in what something *can do*, not just whether it looks malicious (`senior-security`).

They pair with the [Constitution of Agents](https://github.com/mjha-arya/constitution-of-agents) and with [agent-lint](https://github.com/mjha-arya/agent-lint), which checks the same least-privilege ideas statically in your `.claude/` config. This repo passes agent-lint with zero findings.

---
Built by **[Manish Jha](https://github.com/mjha-arya)**, secure and provable AI agents. MIT licensed.
