---
name: ephapax
description: Prevents agents from burning tokens rediscovering already-solved solutions. Enforces a three-phase loop: CHECK for existing deterministic tools first, EXPLORE only when genuinely novel, CODIFY findings so they never need to be reasoned again. Use when the user says "ephapax", "once for all", "don't repeat yourself", "check before reasoning", "don't rediscover", "tokens for discovery only", "codify this", "make this repeatable", "workflow-first", or "discovery mode". Also use when starting any task that might already have a scripted or automated solution.
keywords: [token efficiency, deterministic workflow, agent discipline, codify, check before reasoning, opencode skill, AI cost, avoid re-reasoning, workflow automation, discovery mode]
---

# ephapax: Once for All

> "He entered once for all into the holy places... thus securing an eternal redemption."
> — Hebrews 9:12

---

*Ephapax* (ἐφάπαξ) is Greek for "once for all time." It describes an act so complete that it never needs to happen again. In this skill: reason through a problem once, codify the result, and it stands forever. Do not pay for the same thinking twice.

---

## Fast path

If context is limited, follow only these steps:

1. **State the scan.** Before doing anything, say: `"CHECK: scanning for existing path..."` Then look for scripts, CLIs, runbooks, and pipelines.
2. **Found a path?** Use it. Say: `"CHECK: found <X>. Using it."` Stop.
3. **No path found?** Say: `"CHECK: no path found. Entering EXPLORE."` Declare scope. Reason. Document the finding.
4. **Finding is clear?** Say: `"EXPLORE complete. Finding: <X>. Codifying as <Y>."` Capture it. Verify it. Stop.

---

## The loop

```
CHECK -> EXPLORE -> CODIFY
```

Every task starts at the earliest phase that applies. Do not skip CHECK.

---

## Phase 1: CHECK

Before reasoning, the agent must confirm the scan:

> `"CHECK: scanning for existing deterministic path..."`

Scan in this order:
1. Repo scripts: `Makefile`, `package.json scripts`, `justfile`, `Taskfile`, `scripts/`
2. Available CLIs: `which <tool>`, `--help` flags, installed packages
3. Existing APIs or SDKs the project already depends on
4. Automation config: CI/CD pipelines, linters, migration runners, formatters
5. Runbooks: `CONTRIBUTING.md`, `docs/`, `README.md`

**If a deterministic path exists**, the agent must confirm before using it:
> `"CHECK: found <tool/command>. Using it. No reasoning required."`

Invoke it. Stop. Do not proceed to EXPLORE.

**If no path is found**, the agent must confirm before reasoning:
> `"CHECK: no existing path found. Entering EXPLORE."`

Skipping the CHECK declaration is a protocol violation. If the agent reasons without confirming a scan, stop and restart from CHECK.

---

## Phase 2: EXPLORE

Enter this phase only when CHECK finds nothing and the problem is genuinely novel or uncertain.

**Before exploring**, declare the scope:
> `"Unknown: [X]. Goal: [Y]. I will stop when I have [Z]."`

**While exploring:**
- Prefer evidence (logs, code, docs, tests) over inference
- Use the minimum number of reasoning steps needed
- Do not go beyond the declared scope

**Before leaving EXPLORE**, state the finding:
> `"EXPLORE complete. Finding: [what was learned]. Moving to CODIFY."`

If you cannot state a clear finding, the scope was too broad. Narrow the scope and explore again.

**Record the finding** in a permanent location (code comment, runbook, PR description) before moving on. A finding that is not recorded means the next agent pays the same cost again.

---

## Phase 3: CODIFY

When a behavior is understood and repeatable, capture it so no agent needs to reason through it again.

Choose the simplest form:

| Behavior type | Capture as |
|---|---|
| Single command or sequence | `Makefile` target or `package.json` script |
| Multi-step process with logic | Shell script or language-native script |
| Repeated CLI invocation | Alias, wrapper script, or config flag |
| Deployment or CI steps | Pipeline config (GitHub Actions, etc.) |
| Environment setup | `Dockerfile`, `devcontainer.json`, or setup script |
| Decision process | Runbook in `CONTRIBUTING.md` or `docs/` |
| Agent workflow | OpenCode skill (`.opencode/skills/`) or command (`.opencode/commands/`) |

**Verify before declaring done:**
- Script, Makefile target, or CLI: run it and confirm the output matches the expected result.
- Runbook, doc, or comment: read it back. Can a new agent follow it without reasoning from scratch?

Register the artifact (add to Makefile, link from README, etc.), then tell the user:
> `"Codified as <name>. Future calls use <invocation> directly."`

---

## Example: full loop

> User: "Run the integration tests."

**CHECK.** `"CHECK: scanning for existing path..."` Finds `"test:integration"` in `package.json`.
`"CHECK: found npm run test:integration. Using it."` Runs it. Done.

---

> User: "The integration tests pass locally but fail on CI. Why?"

**CHECK.** `"CHECK: scanning for existing path..."` No script answers this question.
`"CHECK: no existing path found. Entering EXPLORE."`

**EXPLORE.** `"Unknown: why CI diverges from local. Goal: identify one concrete difference. I will stop when I find it."`
Compare CI environment variables, Node version, and file system assumptions.
`"EXPLORE complete. Finding: CI sets NODE_ENV=test, which skips the DB seed step. Moving to CODIFY."`

**CODIFY.** Add a `ci:seed` Makefile target. Document the NODE_ENV requirement in `CONTRIBUTING.md`.
Run `make ci:seed` with `NODE_ENV=test` locally. Tests pass.
`"Codified as 'make ci:seed'. Future CI debugging starts here, not from scratch."`

---

## Anti-patterns

- Reasoning without first declaring `"CHECK: scanning..."`
- Finding a deterministic path but reasoning through it anyway
- Completing EXPLORE without stating a finding
- Stating a finding without recording it in a permanent location
- Codifying without verifying (script: run it; runbook: read it back)
- Staying in EXPLORE past the declared scope


