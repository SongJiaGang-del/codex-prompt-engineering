---
name: codex-prompt-engineering
description: Generate concise, implementation-ready prompts for Codex, Cline, and other coding agents. Use when the user asks to turn requirements, discussions, bug reports, review requests, or architecture ideas into a coding prompt, task specification, engineering blueprint, or verification plan. Do not use for ordinary code implementation unless prompt generation is explicitly requested.
---

# Codex Prompt Engineering

## Overview

Turn incomplete or verbose engineering requests into prompts that a coding agent can execute with minimal ambiguity. Preserve decision-relevant context while removing repetition; correctness, safety, compatibility, and verification take priority over token minimization.

## Trigger Boundary

Use this skill when the requested output is a prompt, task brief, implementation specification, coding blueprint, or prompt rewrite.

Do not let this skill replace specialized workflows for implementation, debugging, code review, security, testing, UI design, research, or document creation. In those cases, use this skill only when the user explicitly asks to improve the prompt or task specification.

## Construction Workflow

Follow this sequence:

1. Extract the desired outcome and rewrite it as one measurable objective.
2. Separate required behavior, implementation suggestions, and non-goals.
3. Identify repository facts, files, modules, routes, interfaces, data models, and runtime assumptions.
4. State constraints, compatibility requirements, and negative requirements.
5. Define edge cases, failure behavior, and state transitions when relevant.
6. Define concrete verification commands and acceptance criteria.
7. Label bounded assumptions and unresolved questions.
8. Remove repetition and vague wording without removing information that affects an implementation decision.

Never invent repository paths, APIs, dependencies, test results, or product behavior. If repository inspection is required, instruct the coding agent to inspect the repository before editing.

## Prompt Format

Output only sections that contain useful information:

### Context

Relevant product, repository, architecture, existing behavior, and prior decisions.

### Objective

One concrete implementation outcome.

### Scope

Required changes and explicitly excluded changes.

### Files and Interfaces

Known files, modules, routes, types, schemas, function signatures, and ownership boundaries. If unknown, state what must be discovered.

### Constraints

Compatibility, dependency, performance, security, migration, style, and backward-compatibility requirements. Include negative constraints such as "Do not change the public API" or "Do not remove legacy behavior before parity is verified."

### Implementation Requirements

Behavioral rules, edge cases, error handling, and integration details. Do not over-prescribe internal design when repository conventions should determine it.

### Verification

Concrete tests, type checks, build commands, browser workflows, static checks, or manual acceptance checks. Distinguish source-level evidence from runtime evidence.

### Deliverables

Expected code changes, tests, documentation, migration files, reports, or screenshots.

### Assumptions and Questions

Label assumptions explicitly. Ask questions only when different answers would materially change architecture, data, security, or user-visible behavior.

Omit empty sections. Keep the final prompt ready to paste into a coding agent.

## Task Modes

Adapt the prompt to the requested mode:

- Implement: behavior, scope, interfaces, tests, and acceptance criteria.
- Fix: symptoms, reproduction, evidence, suspected root cause, regression test, and fix boundaries.
- Refactor: invariants, compatibility requirements, allowed structural changes, and regression checks.
- Review: review scope, standards, risk priorities, and required finding format.
- Design: alternatives, decision criteria, tradeoffs, and selected direction.
- Research: authoritative sources, questions to answer, and required evidence format.

## Quality Rules

- Use exact names and signatures when known.
- Replace vague terms such as "properly" or "make it better" with observable behavior.
- Define failure behavior, not only the happy path.
- Distinguish must-have requirements from suggestions.
- Keep unrelated background out of the prompt.
- Make each acceptance criterion independently checkable.
- Do not promise completion unless the specified verification has passed.
- Prefer focused diffs and precise anchors for code-edit instructions.
- Provide complete files only for new files or when explicitly requested.

## Output Style

When the user asks for a prompt, provide the ready-to-use prompt first. Keep any explanation brief and separate. Avoid greetings, generic advice, and motivational text.
