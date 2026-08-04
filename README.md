# Just Enough

**Stop coding agents from turning a two-line fix into a framework.**

Just Enough is a tiny, model-agnostic Agent Skill for controlling scope, test loops, speculative abstractions, and unrequested polish.

> Smallest sufficient change. Proportionate proof. Then stop.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## The problem

Powerful coding agents often keep improving after the task is already solved. A narrow fix grows into a refactor. One useful test becomes the full suite, then the same suite again. A review finds adjacent cleanup, and the agent quietly adopts it as new scope.

"Don't overengineer" is too vague. Just Enough gives the agent an executable stopping policy:

1. Lock the requested outcome, scope, constraints, and proof.
2. Make the smallest sufficient change at the narrowest ownership boundary.
3. Match verification effort to actual risk.
4. Separate in-scope blockers from adjacent improvements.
5. Stop when the outcome is proven.

## Install

The repository contains one portable skill at [`skills/just-enough`](skills/just-enough).

With a recent GitHub CLI that supports Agent Skills:

```sh
gh skill install chocota001/just-enough just-enough
```

For manual installation, copy `skills/just-enough` into a skills directory supported by your agent. Common project-level locations include:

```text
.agents/skills/just-enough/
.github/skills/just-enough/
.claude/skills/just-enough/
```

Personal skill locations vary by host. Inspect the single `SKILL.md` before installing; this project contains no executable scripts, hooks, network calls, or tool permissions.

## Use

Invoke the skill explicitly when you want a hard scope boundary:

```text
Use $just-enough to fix the mobile menu regression. Do not redesign the header.
```

Or install it at project scope and let a compatible agent load it when the task risks scope creep or excessive verification.

## Before and after

**Without a stopping policy**

```text
Fix the null title crash.
→ Reworks the content model
→ Adds a validation framework
→ Migrates unrelated call sites
→ Runs the full suite three times
```

**With Just Enough**

```text
Fix the null title crash.
→ Reproduces the crash
→ Patches the existing title boundary
→ Adds or runs one focused regression check
→ Reports the proof and stops
```

## What it will not do

Just Enough does not lower the bar for security, data integrity, public API changes, migrations, or releases. It preserves explicit acceptance criteria and mandatory repository checks. If the user asks for an exhaustive audit or a broad refactor, that broader scope remains authoritative.

## Compatibility

The skill uses the open `SKILL.md` format and has no runtime dependencies. It is designed for Codex, Claude Code, GitHub Copilot, and other Agent Skills-compatible tools.

This is an independent community project. It is not affiliated with or endorsed by OpenAI, Anthropic, GitHub, Microsoft, or any model provider. It does not reproduce proprietary prompts or claim that any named model always behaves in a particular way.

## Contributing

Small, evidence-backed improvements are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md). In the spirit of the project, proposals should solve an observed failure mode without turning the skill into a general software-engineering handbook.

## License

MIT. See [LICENSE](LICENSE).
