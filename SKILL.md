---
name: codex-prompt-engineering
description: Turn requirements or discussions into coding-agent prompts, task specifications, or verification plans. Use when the requested deliverable is a prompt or task brief, including prompt rewrites and cross-agent handoffs. Do not take over ordinary implementation, debugging, review, or design work.
---

# Codex Prompt Engineering

Turn engineering requests into task briefs that preserve intent, evidence, and acceptance conditions. Remove repetition without losing information that changes an implementation decision.

## Scope and Output Size

Use this skill when the deliverable is a prompt, task brief, implementation specification, coding blueprint, or prompt rewrite. It does not replace implementation, debugging, code review, security, testing, UI design, research, or document workflows. A review prompt remains a request to review, not authorization to fix findings.

Choose the smallest useful form, considering ambiguity and consequence as well as task size:

- **Short instruction:** A bounded, well-understood change. Use a paragraph or a few bullets covering the outcome, limits, and proportionate verification. Do not add headings, tests, or process solely to fill a template.
- **Structured brief:** Multiple behaviors, interfaces, compatibility limits, or acceptance conditions need coordination. Select useful sections from the format below.
- **Discovery brief:** The goal, root cause, or a material contract is unresolved. Specify what to inspect, questions to settle, and evidence needed before dependent implementation. Complete any independent, authorized scope; do not invent a solution to make the brief look executable.

Honor the user's requested format. If an existing specification is sufficient, make the requested correction or extract the current task instead of rewriting everything. Consult [examples](references/examples.md) only when an example would help choose the level of detail.

## Preserve Facts and Decisions

Before drafting, distinguish the following where confusing them could affect the work:

- **Requirement:** Behavior or a boundary explicitly requested by the user. Preserve exact names, values, exclusions, and the scope of any approval.
- **Verified fact:** Supported by inspected source or observed output. Keep a compact source anchor for decision-critical facts, such as a file and symbol, document section, or observed command and result. Preserve relevant revision or environment limits; do not imply an old observation is current.
- **Reported or unresolved:** A user-reported symptom, uninspected repository claim, or hypothesis. Attribute it and state what would confirm or disprove it. A suspected cause must not become an instruction to implement that cause's presumed fix.
- **Suggestion:** An optional implementation approach. Leave internal design to repository conventions unless the user has made it a requirement.

Use plain labels only where needed; a small task does not need a facts table. Never invent paths, APIs, dependencies, commands, test results, or product behavior. Inspect relevant available sources when needed to ground the brief; otherwise identify what the execution agent must discover before editing.

For long discussions, reconcile revisions before compression. A later explicit revision of the same requirement replaces the earlier version; unrelated later remarks do not cancel existing limits. Exclude withdrawn decisions from active requirements, retaining a short "superseded" note only when it prevents likely reintroduction. Preserve unresolved conflicts rather than choosing silently.

Ask a focused question when an unresolved choice would materially change architecture, data, security, or user-visible behavior and cannot be settled by inspection. When the requested deliverable is a handoff, include that question and the dependent work boundary in the brief; the receiving agent must settle it before acting on that part. Do not turn a request to draft a prompt into permission to perform its implementation or external actions.

## Construct the Brief

State one coherent outcome, separating required behavior, optional approaches, and non-goals. Add relevant failure behavior and state transitions, not speculative edge cases. Use observable behavior instead of "properly" or "make it better."

For a structured brief, include only useful sections:

- **Context:** Relevant product behavior, source anchors, and current decisions.
- **Objective:** The concrete outcome of this task or discovery phase.
- **Scope:** Required changes, ownership boundaries, exclusions, and preserved behavior.
- **Files and Interfaces:** Known paths, routes, signatures, schemas, and contracts; explicit discovery work for unknowns.
- **Constraints:** Applicable compatibility, dependency, migration, performance, security, or style requirements.
- **Implementation Requirements:** Behavioral rules, integration details, and relevant failure handling without unnecessary internal design prescriptions.
- **Verification:** Independently checkable acceptance conditions and the evidence needed for each.
- **Deliverables:** Requested changes and supporting artifacts, scaled to the work.
- **Assumptions and Questions:** Remaining uncertainty and which dependent work must wait for resolution.

Adapt the substance to the task; these modes describe prompt content, not extra workflows to run:

- **Implement:** Required behavior, interfaces, failure cases, and acceptance.
- **Fix:** Reported symptoms, reproduction evidence, hypotheses to test, fix boundaries, and proportionate regression coverage. Distinguish authorized, reversible diagnostic experiments from applying an unproven fix; an uncertain root cause is not a blanket ban on testing a hypothesis.
- **Refactor:** Preserved behavior, compatibility, allowed structural changes, and regression checks.
- **Review:** Review scope or baseline, standards, risk priorities, and actionable finding format.
- **Design:** Alternatives, decision criteria, tradeoffs, and whether a direction is selected or still open.
- **Research:** Questions, authoritative sources, and required evidence format.

## Make Verification Executable and Honest

For each material acceptance condition, specify observable evidence and an appropriate check. Reuse commands only when supplied or discovered; when unknown, direct the agent to discover the relevant scripts, environment, and invocation first. Do not assume a package manager, browser, account, service, or test runner is available.

Match verification to the change. A small reversible edit may need a focused diff or visual check; behavior changes may need targeted tests and runtime checks. Do not require unrelated suites, screenshots, or new tests solely because they appear in the format.

Keep these states distinct when reporting existing evidence or instructing the receiver to report results:

- **Planned:** A check or acceptance condition to perform; no result is implied.
- **Verified:** An observed result with its evidence and scope. Source inspection, build success, test results, and browser interaction establish different things.
- **Unverified or blocked:** A check was not performed or could not be completed. State the reason and remaining acceptance gap. A fallback check may add evidence but cannot silently replace required runtime or human acceptance.

A completed prompt is a deliverable, not proof that the described implementation has passed. Do not carry forward a success, approval, or freeze claim beyond the evidence or scope supporting it.

## Check for Lost or Added Requirements

Before returning the prompt, compare it with the source request and current decisions:

- Every required behavior, prohibition, exact identifier or value, approval limit, and acceptance condition is retained or explicitly unresolved.
- No hypothesis, suggestion, withdrawn decision, or new external action has become an authorized requirement.
- Each material unknown has a discovery step or question, and dependent work has a clear boundary.
- Repetition and irrelevant background are removed without deleting decision-critical evidence.

This is a content check, not a requirement to print another checklist. Include a compact requirement-to-section mapping only when requested or when a complex handoff needs traceability.

## Delivery

Provide the ready-to-use prompt first, in the user's language unless requested otherwise. State each constraint once, referring back only when useful; avoid repeating the same caveat under context, implementation, verification, and deliverables. Keep any explanation brief and separate; omit empty sections, greetings, and generic advice. For code-edit briefs, prefer focused diffs and known anchors; request complete files only for new files or when explicitly requested.
