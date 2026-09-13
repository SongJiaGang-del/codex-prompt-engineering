# Codex Prompt Engineering

[简体中文](README.md) | **English**

Turn requirements, discussions, and bug reports into task prompts you can hand to a coding agent. Preserve the facts, current decisions, allowed changes, and acceptance conditions that matter to implementation.

Use it for complex requests and handoffs between tasks. The behavior is defined in [SKILL.md](SKILL.md). Start with a short example below, or inspect the [recorded outputs and revisions](evals/2026-09-13-results.md) (Chinese).

## Quick start

### 1. Install in Codex

If your Codex environment provides `$skill-installer`, send this request. Already installed? Skip to the next step.

```text
Use $skill-installer to install codex-prompt-engineering from:
https://github.com/SongJiaGang-del/codex-prompt-engineering
SKILL.md is at the repository root. Use codex-prompt-engineering as the installation name.
```

This repository provides Codex skill instructions and interface metadata. You can also give the resulting prompts to Cline or other coding agents. Their native skill loading and compatibility have not been verified here.

### 2. Provide your request

Try this fictional example:

```text
Use $codex-prompt-engineering to turn this requirement into a task prompt for another agent:

The profile page sometimes displays old values after saving; refreshing fixes the display.
I suspect caching, but have not collected logs.
Diagnose first, then make the smallest frontend fix supported by evidence.
Do not change the backend or add dependencies.
File locations and test commands are unknown; the receiving agent should inspect the repository.
Generate the prompt only. Do not diagnose or modify the project in this task.
```

For an existing conversation:

```text
Use $codex-prompt-engineering to turn our discussion into the next implementation task.
Preserve the latest explicit decisions, approved scope, exclusions, and acceptance requirements.
Identify unresolved questions and the work that depends on their answers.
```

### 3. Check and hand off

The output starts with the ready-to-use prompt. Check its facts, scope, and unresolved questions before handing it to the execution agent. Implementation still requires inspecting the actual repository and verifying behavior with the available tools and environment.

## When to use it

Use it to prepare implementation prompts, condense long discussions, organize diagnostic tasks, or define a refactoring or review brief.

For a clear, simple task, direct execution may be enough. This skill does not replace implementation, debugging, security review, testing, UI design, research, or documentation workflows. Asking it to write a review prompt does not authorize fixing the eventual findings.

## Three forms, chosen to fit the task

| Form | Best fit | Output |
| --- | --- | --- |
| Short instruction | A bounded, well-understood change | A paragraph or a few bullets: outcome, limits, proportionate verification |
| Structured brief | Several behaviors, interfaces, or acceptance conditions | Relevant context, decisions, scope, contracts, implementation requirements, and checks |
| Discovery brief | An unresolved goal, root cause, or material contract | What to inspect, evidence to collect, and which implementation work depends on the findings |

Only useful sections are included. An existing specification can receive a focused correction instead of a complete rewrite. See [three worked examples](references/examples.md), currently in Chinese.

For a fictional one-line request, the result can stay short:

> Change the login button from "OK" to "Log in" in src/pages/Login.vue. Only change that text; check the diff, with no browser run or new tests.

An illustrative handoff:

```text
In src/pages/Login.vue, locate the login form's submit button and replace "OK" with "Log in".
Change only that text. Preserve styles, click behavior, and all other files. Check the diff and report the result; do not launch a browser or add tests.
```

## What the brief should preserve

- Requirements, inspected facts, reported symptoms, hypotheses, and suggestions remain distinguishable.
- Later explicit revisions replace earlier decisions without discarding unrelated boundaries.
- Unknown paths, interfaces, dependencies, and commands require discovery, rather than invented details.
- Suspected causes remain hypotheses. Authorized, reversible diagnostic experiments can still test them.
- Planned checks, observed results, and unverified acceptance conditions stay separate. Source inspection, tests, browser interaction, and human approval establish different things.

Provide expected behavior, permitted changes, exclusions, known contracts, evidence, and acceptance requirements when available. Mark missing information as unknown; there is no need to fill every section first.

## Validation and limits

On September 13, 2026, the repository received structure and link checks, plus prompt-generation spot checks using three fictional cases. Four outputs were retained:

- A small edit and a discussion with revised requirements were each run once. Their key scope and acceptance conditions were preserved.
- The uncertain-root-cause case initially restricted diagnostic experiments too broadly. After a targeted revision, a new independent agent reran that case; the same restriction was not observed in that output.
- The first two cases were not rerun on the final candidate. Their earlier results do not establish a complete regression pass for that version.

Read the [method and cases](evals/README.md) and [outputs, findings, and retest record](evals/2026-09-13-results.md), currently in Chinese.

This is an instruction-only skill with no additional execution tools. No real-project comparison against direct execution or a generic template has been completed. There is no demonstrated improvement in coding success rates, token costs, or total time. These samples also do not establish reliable behavior across repeated runs. A completed prompt is not evidence that its implementation is complete or accepted.

## Feedback

If this is useful to you, consider starring the repository. Failure cases are welcome in [GitHub Issues](https://github.com/SongJiaGang-del/codex-prompt-engineering/issues): include a redacted original request, generated prompt, and what was omitted, invented, or unnecessarily constrained. Model and environment details help when available.

## License

This repository currently has no declared standalone license.
