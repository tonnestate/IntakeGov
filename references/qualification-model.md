# Qualification Model

This reference defines when a request is sufficiently understood for its next stage.

The model is intentionally stage-relative. A discovery request does not need implementation-level detail; an implementation request often does.

## General sufficiency test

A request is `SUFFICIENT` when all information required to choose and safely enter the next delivery stage is known, and no unresolved gap is likely to materially change that stage.

A request is `INSUFFICIENT` when a missing answer can materially change scope, project relation, architecture, risk, licensing, feasibility, or success criteria.

## Qualification dimensions

Evaluate only dimensions relevant to the request.

### Outcome

What must be true when the work succeeds?

### User / actor

Who experiences the result or operates the system?

Required when user behavior, permissions, experience, workflow, or value depends on the actor.

### Problem

What problem or opportunity is being addressed?

Required for product bets, new products, and solution-first requests whose real need is unclear.

### Scope

What is explicitly in scope and out of scope?

Required when boundaries can materially change the work.

### Existing context

What project, codebase, system, environment, process, or prior decision already exists?

Required when the work may extend something already built.

### Constraints

Examples:

- required languages or platforms;
- hosting/runtime constraints;
- budget;
- deadlines;
- data locality;
- compliance;
- backward compatibility;
- organizational constraints.

Require only constraints that affect the route or design.

### Success criteria

How will the result be judged?

For implementation, this should normally produce testable or observable acceptance conditions.

### Inputs / outputs

Required when interfaces, data flows, files, APIs, transformations, or integrations are material.

### Risk

Identify material security, privacy, financial, legal, operational, safety, or irreversible effects.

### External dependencies

Identify whether packages, repositories, models, data, services, templates, skills, or assets may be incorporated.

## Examples

### Insufficient

> I want an app.

Unknown outcome, users, problem, project relation, scope, platform, and success state.

Result:

- `PROJECT_RELATION: NEW_PROJECT_CANDIDATE` only if context supports it;
- `WORK_SCALE: UNKNOWN`;
- `UNDERSTANDING: INSUFFICIENT`;
- execution blocked.

### Sufficient for discovery, not implementation

> We want a lightweight internal tool for 20 support agents to classify incoming PDF complaints and assign them to one of five teams. We do not yet know whether OCR/LLM classification is reliable enough.

This is sufficient to route to investigation/product discovery even though implementation details remain unresolved.

### Sufficient for bounded change

> In the existing CRM contact list, add CSV export of the currently filtered rows. Preserve the visible column order. UTF-8 with header row. No background job. Existing authorization rules apply.

This can be sufficient for an existing-project feature/change after project context is loaded.

## Clarification discipline

Ask the smallest number of questions that removes material ambiguity.

Prefer questions that eliminate entire branches of possible execution.

Do not ask for implementation detail before the product or outcome is understood.

Do not ask the user to repeat information already available in project context.
