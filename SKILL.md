---
name: intake-gov
description: Always-first intake and routing skill for requests that may create, change, extend, investigate, replace, release, or substantially modify a product, project, system, application, feature, integration, workflow, or reusable artifact. Classifies the work before execution, resolves project context, asks only necessary clarification questions, blocks premature implementation, selects an appropriate delivery path, and requires license/provenance review before external artifacts are reused.
license: Apache-2.0
metadata:
  version: "0.1.0"
  status: experimental
  category: governance
  updated: "2026-09-15"
---

# IntakeGov

IntakeGov is a project and product intake governor for AI agents.

Its purpose is not to do the work itself. Its purpose is to ensure the agent understands what kind of work is being requested, whether the work belongs to an existing project or a new one, whether the request is sufficiently specified, and which delivery workflow should handle it.

## Core invariant

Treat every substantive request as `UNCLASSIFIED_WORK` until it has been classified.

Do not assume that a vague request is a new project, a feature, a coding task, or a research task.

Do not begin substantial execution until the request has a valid intake state.

## Why this skill exists

AI agents frequently make one of four mistakes:

1. They turn vague intent into an implementation without sufficient qualification.
2. They create a new architecture for work that belongs to an existing project.
3. They use the wrong delivery process for the size or risk of the request.
4. They reuse external code, packages, templates, skills, assets, or repositories without a verified license and provenance decision.

IntakeGov prevents these failures before execution begins.

## Invocation

Invoke this skill before substantial execution when a request may:

- create a product, application, service, system, repository, workflow, integration, feature, or reusable component;
- change or extend an existing project;
- start an investigation that can lead to implementation;
- introduce an external dependency, repository, package, skill, template, dataset, model, asset, or codebase;
- require architecture, product discovery, requirements work, multi-step delivery, or cross-system coordination.

Do not invoke full project ceremony for ordinary factual questions, simple explanations, or clearly bounded conversational requests that have no project or execution implications.

Runtime environments that require deterministic always-first behavior should install the global invocation rule described in `references/runtime-integration.md`.

## Hard rules

### 1. No premature execution

Until intake is sufficiently qualified:

- do not choose a technology stack;
- do not finalize architecture;
- do not generate substantial implementation code;
- do not create a repository structure;
- do not launch broad prior-art research;
- do not treat assumptions as requirements.

Context retrieval that is necessary to determine whether the request belongs to an existing project is allowed.

### 2. Existing project context comes before new-project assumptions

If the request plausibly belongs to an existing project, load or inspect the available project context before classifying it as a new project.

Never create a parallel project merely because the current request is phrased independently.

### 3. Clarify only material uncertainty

Do not ask a generic questionnaire.

Ask only questions whose answers can materially change:

- project relation;
- scope;
- success criteria;
- architecture;
- delivery route;
- risk;
- legal or licensing treatment;
- implementation feasibility.

Prefer the smallest set of high-information questions.

### 4. No hidden scope creation

Do not silently add features, systems, integrations, infrastructure, databases, frameworks, or redesigns that the request does not require.

Record assumptions explicitly when assumptions are unavoidable and obtain clarification when the assumption is material.

### 5. No external reuse without license and provenance status

Any external artifact considered for reuse must have a provenance and license decision before it enters a deliverable.

Unknown, missing, conflicting, or scope-unclear licensing must never be treated as permission.

See `references/license-provenance-gate.md`.

### 6. Build is not the default

When implementation is likely, route the qualified request through a prior-art/reuse step before substantial custom implementation unless the request is clearly trivial or prior art cannot materially affect the solution.

The prior-art integration contract is defined in `references/prior-art-hook.md`.

### 7. Route proportionally

Do not impose project-scale process on a simple question or atomic change.

Do not use a lightweight direct-execution path for work that has unresolved product, architecture, security, licensing, or cross-system consequences.

## Intake state

Maintain the following state for substantive requests.

### `REQUEST_NATURE`

One of:

- `QUESTION`
- `ACTION`
- `CHANGE`
- `INVESTIGATION`
- `IDEA`
- `PRODUCT_BET`
- `INCIDENT`
- `UNKNOWN`

### `PROJECT_RELATION`

One of:

- `NO_PROJECT`
- `STANDALONE`
- `EXISTING_PROJECT`
- `NEW_PROJECT_CANDIDATE`
- `UNKNOWN`

### `WORK_SCALE`

One of:

- `ATOMIC_TASK`
- `CHANGE`
- `FEATURE`
- `EPIC`
- `PROJECT`
- `UNKNOWN`

### `UNDERSTANDING`

One of:

- `INSUFFICIENT`
- `SUFFICIENT`

### `DELIVERY_READINESS`

One of:

- `NOT_READY`
- `READY`

### `EXECUTION_STATE`

One of:

- `BLOCKED`
- `DIRECT`
- `ROUTED`

### Additional flags

Maintain when relevant:

- `PRIOR_ART_REQUIRED`: `true|false`
- `LICENSE_REVIEW_REQUIRED`: `true|false`
- `PRODUCT_DISCOVERY_REQUIRED`: `true|false`
- `ARCHITECTURE_REVIEW_REQUIRED`: `true|false`
- `SECURITY_REVIEW_REQUIRED`: `true|false`
- `HUMAN_DECISION_REQUIRED`: `true|false`

## Intake procedure

### Step 0 — Determine whether intake is needed

If the request is a simple factual question or explanation with no project implication, classify:

- `REQUEST_NATURE: QUESTION`
- `PROJECT_RELATION: NO_PROJECT`
- `WORK_SCALE: ATOMIC_TASK`
- `UNDERSTANDING: SUFFICIENT`
- `DELIVERY_READINESS: READY`
- `EXECUTION_STATE: DIRECT`

Answer directly.

Otherwise continue.

### Step 1 — Resolve project context

Determine whether the request belongs to an existing project.

Use available project context, repository context, workspace metadata, user-provided references, or persistent project memory when available.

If relation is unclear and materially changes the work, clarify it.

Do not infer `NEW_PROJECT_CANDIDATE` merely because no project name was supplied.

### Step 2 — Identify the intended outcome

Determine what must be true when the work is successful.

Separate:

- outcome;
- requested solution;
- constraints;
- assumptions.

A requested solution is not automatically the real requirement.

Example:

`"I need an app"` is not a qualified outcome.

### Step 3 — Classify request nature

Use the classification rules in `references/work-classification.md`.

When multiple categories apply, select the category that best describes the decision that must happen before execution.

### Step 4 — Check requirement sufficiency

Use `references/qualification-model.md`.

A request is sufficient only when the missing information can no longer materially alter the selected delivery route or invalidate the next work stage.

Do not require exhaustive specification before discovery or investigation.

Sufficiency is stage-relative.

### Step 5 — Clarify material gaps

If `UNDERSTANDING: INSUFFICIENT`:

- set `DELIVERY_READINESS: NOT_READY`;
- set `EXECUTION_STATE: BLOCKED`;
- ask the minimum necessary question or questions;
- stop before implementation.

Do not compensate for missing information by inventing requirements.

### Step 6 — Determine work scale

Classify using impact, uncertainty, number of subsystems, architectural reach, coordination needs, risk, and expected delivery depth.

Do not size by estimated code lines alone.

See `references/work-classification.md`.

### Step 7 — Determine whether product discovery is required

Set `PRODUCT_DISCOVERY_REQUIRED: true` when the request is a new product, product bet, uncertain user problem, uncertain value proposition, or a substantial feature whose value is not established.

Product discovery should answer whether the proposed work should be built before engineering effort is committed.

### Step 8 — Determine whether prior art is required

Set `PRIOR_ART_REQUIRED: true` when existing libraries, packages, repositories, frameworks, systems, reference implementations, standards, or internal exemplars can materially change the implementation decision.

Do not launch broad prior-art research until the capability or problem is sufficiently qualified.

### Step 9 — Trigger license/provenance review when external artifacts are considered

Set `LICENSE_REVIEW_REQUIRED: true` when an external artifact may be:

- copied;
- modified;
- vendored;
- distributed;
- embedded;
- used as a template;
- installed as a dependency;
- included in generated output;
- used as a reusable skill or agent resource.

Pure conceptual reference still requires source tracking when the distinction between learning and derivation could matter.

### Step 10 — Select the delivery route

Use `references/routing-model.md`.

The route must fit the work instead of forcing all work through one methodology.

### Step 11 — Permit execution

Execution may become `DIRECT` or `ROUTED` only when:

- project relation is known sufficiently for the current stage;
- understanding is sufficient for the next stage;
- the delivery route is selected;
- mandatory gates have been identified;
- no unresolved blocking license/provenance issue exists for artifacts already selected for reuse.

Otherwise execution remains `BLOCKED`.

## User-facing behavior

Do not dump the entire intake state unless the user asks for it or the state is necessary to explain a routing decision.

When clarification is required, ask concise, decision-relevant questions.

When intake is complete, proceed through the selected route rather than narrating project-management theory.

Do not turn IntakeGov into ceremony.

## Minimum routing outcomes

IntakeGov must be able to route to at least these execution modes:

### Direct answer

For factual questions and explanations.

### Direct bounded execution

For small, unambiguous, low-risk work with no meaningful project or architecture uncertainty.

### Existing-project change

Load project context, confirm affected scope, then use a disciplined implementation and verification workflow.

### Feature specification

For bounded but non-trivial features requiring requirements, acceptance criteria, planning, and verification.

### Project planning

For multi-feature, multi-system, architecture-heavy, or coordinated work.

### Product discovery

For new products, product bets, unclear value, unclear user problem, or uncertain build justification.

### Investigation / research

For questions where evidence gathering must precede a build decision.

### Incident / repair

For production breakage or urgent defects where restoration and containment precede normal discovery.

### Prior-art / reuse evaluation

For qualified capabilities where existing software may provide a better base than custom implementation.

## Required external-reuse decision

Before an external artifact is incorporated into a deliverable, one of these states must exist:

- `REFERENCE_ONLY`
- `PATTERN_ONLY`
- `DEPENDENCY_ALLOWED`
- `CODE_REUSE_ALLOWED`
- `REVIEW_REQUIRED`
- `DENIED`

No decision means no reuse.

## Completion criteria

IntakeGov completes when one of these is true:

1. The request is classified as direct, non-project work and execution may proceed.
2. The request is sufficiently qualified and routed to an appropriate delivery workflow.
3. The request remains blocked and the exact missing information is requested.
4. An external-reuse attempt is blocked by license/provenance policy.
5. The request is rejected or deferred because a mandatory product, legal, security, or human decision is unresolved.

IntakeGov does not claim that the downstream implementation is complete.

## Anti-patterns

Never do the following:

- `"I want an app"` → immediately select React/FastAPI/PostgreSQL.
- `"Add a button"` → create a new project without checking existing context.
- `"Research GitHub"` → scrape broadly without knowing what decision the research serves.
- `"Use this repo"` → copy code before verifying provenance and license scope.
- `"It's MIT"` → assume every file, asset, dependency, or embedded artifact is MIT.
- `"This is small"` → bypass architecture or security impact that is clearly material.
- `"This is a project"` → impose heavy planning on a simple answer or atomic change.

## References

Read these files when the corresponding decision is required:

- `references/qualification-model.md`
- `references/work-classification.md`
- `references/routing-model.md`
- `references/license-provenance-gate.md`
- `references/prior-art-hook.md`
- `references/runtime-integration.md`
