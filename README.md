# ephapax

*Once for all.*

*Ephapax* (ἐφάπαξ) is a Greek word used in the New Testament to describe an act done so completely and finally that it never needs to be repeated. One act. Settled forever.

That is the discipline this skill enforces. Reason through a problem once. Codify the result. It stands forever. The same cognition must never be paid for twice.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

---

## The problem

You ask an agent to run the tests. It spends 800 tokens reasoning about how to run tests: checks the language, infers the framework, constructs the command, and arrives at `npm test`.

You ask again tomorrow. It does the same thing. 800 more tokens. Same answer.

You are paying for cognition that produces no new information. The answer was already known. It just was not captured anywhere a machine could find without thinking.

This is the problem `ephapax` solves.

---

## Why it happens

Agents are general-purpose reasoners. They handle what they have never seen before very well: uncertainty, ambiguity, novel problems, edge cases.

The mistake is using that same machinery for problems that have already been solved. Once something is understood and repeatable, an agent reasoning through it again produces nothing new. It just burns tokens to reach the same answer.

Agents should handle uncertainty, exploration, and exceptions. Once a behavior becomes understood and repeatable, it should be captured in deterministic code, API/CLI tools, or workflows — not reasoned through again from scratch.

The goal is not to eliminate agents. It is to stop paying for the same cognition over and over again. Tokens should fund discovery, not rent-seeking on already-solved problems.

---

## The fix: a three-phase discipline

```
CHECK -> EXPLORE -> CODIFY
```

**CHECK.** Before reasoning about anything, look for a deterministic path that already exists. A Makefile target. A CLI command. An existing script. A runbook. If it exists, use it. Stop there.

**EXPLORE.** If no path exists, reason through it. Declare the scope before you start, and document what you learn before you stop. A finding that is not recorded means the next session pays the same cost again.

**CODIFY.** Once something is understood, capture it in a form that requires no reasoning to use: a script, a pipeline step, a runbook entry, an OpenCode skill. Verify it works. Register it. It now costs nothing to use again.

---

## What this is not

This is not about replacing agents with scripts. Agents are essential for exploration, debugging unknown systems, handling exceptions, and designing things that have never been built before. That work justifies every token.

The discipline is about where agents are deployed. On the frontier of what is not yet known, not on ground that already has a Makefile target.

---

## Cost model

| Situation | Token cost | Correct action |
|---|---|---|
| Solved, deterministic path exists | ~0 | CHECK: use it |
| Novel, genuinely uncertain | Justified | EXPLORE: reason, document |
| Solved, but agent re-reasons anyway | Full cost, zero value | Should have been Codified |

---

## Install

### Manual install

Copy `SKILL.md` to the skills directory of your agent.

| Agent | Path |
|---|---|
| OpenCode | `.opencode/skills/ephapax/SKILL.md` |
| Claude Code | `.claude/skills/ephapax/SKILL.md` |
| Codex CLI | `.agents/skills/ephapax/SKILL.md` |
| Cursor | `.cursor/skills/ephapax/SKILL.md` |
| Gemini CLI | `.gemini/skills/ephapax/SKILL.md` |
| GitHub Copilot | `.github/skills/ephapax/SKILL.md` |
| Windsurf | `.windsurf/skills/ephapax/SKILL.md` |
| Cline | `.cline/skills/ephapax/SKILL.md` |
| Roo Code | `.roo/skills/ephapax/SKILL.md` |
| Amp | `.agents/skills/ephapax/SKILL.md` |
| Hermes Agent | `~/.hermes/skills/ephapax/SKILL.md` |
| OpenClaw | `~/.openclaw/skills/ephapax/SKILL.md` |
| Kiro CLI | `~/.kiro/skills/ephapax/SKILL.md` |
| Factory Droid | `.factory/skills/ephapax/SKILL.md` |

Agents without native skill directories (Aider, for example) can read the prompt with `/read <path/to/SKILL.md>`. The Markdown prompt works with any LLM.

---

## Agent compatibility

| Agent | Skill support | Notes |
|---|---|---|
| OpenCode | Native | Auto-loads from `.opencode/skills/` |
| Claude Code | Native | Auto-loads from `.claude/skills/` |
| Codex CLI | Manual | Paste or `/read` |
| Cursor | Manual | Paste or `/read` |
| Gemini CLI | Manual | Paste or `/read` |
| GitHub Copilot | Manual | Paste or `/read` |
| Windsurf | Manual | Paste or `/read` |
| Cline | Manual | Paste or `/read` |
| Roo Code | Manual | Paste or `/read` |
| Amp | Manual | Paste or `/read` |
| Hermes Agent | Manual | Paste or `/read` |
| Kiro CLI | Manual | Paste or `/read` |

---

## License

MIT — see [LICENSE](./LICENSE).

---

> "He entered once for all into the holy places... thus securing an eternal redemption."
> — Hebrews 9:12
