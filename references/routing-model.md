# Routing Model

IntakeGov selects a delivery route. It does not require any specific third-party framework.

Integrations may map these generic routes to BMAD, Superpowers, Spec Kit, internal workflows, or other compatible methods.

## Route: `DIRECT_ANSWER`

Use for:

- factual questions;
- explanations;
- simple comparisons;
- non-project conversation.

Required state:

- `REQUEST_NATURE: QUESTION`
- sufficient understanding.

## Route: `DIRECT_BOUNDED_EXECUTION`

Use for:

- atomic, unambiguous, low-risk actions;
- no material architecture or product uncertainty;
- no unresolved external-reuse issue.

Verification is still required when a change is made.

## Route: `EXISTING_PROJECT_CHANGE`

Use when:

- `PROJECT_RELATION: EXISTING_PROJECT`;
- work is `CHANGE` or bounded `FEATURE`.

Required behavior:

1. load project context;
2. identify affected components;
3. define acceptance conditions;
4. run prior-art/reuse check when relevant;
5. implement;
6. verify against existing behavior.

## Route: `FEATURE_SPECIFICATION`

Use for bounded non-trivial features.

Typical flow:

1. clarify;
2. specify behavior;
3. define acceptance criteria and edge cases;
4. identify architecture impact;
5. evaluate prior art;
6. plan;
7. implement;
8. verify.

## Route: `PROJECT_PLANNING`

Use for `PROJECT` or substantial `EPIC`.

Typical flow:

1. establish objective and non-goals;
2. product/discovery work if value is uncertain;
3. architecture/context analysis;
4. capability decomposition;
5. prior-art evaluation;
6. milestones/epics;
7. delivery plan;
8. execution;
9. verification;
10. release and learning.

## Route: `PRODUCT_DISCOVERY`

Use for:

- new product;
- product bet;
- unclear user/problem;
- unclear value;
- solution-first request with unverified assumptions.

This route must be allowed to conclude:

- build;
- prototype;
- investigate;
- defer;
- do not build.

## Route: `INVESTIGATION`

Use when evidence must precede an implementation decision.

The output should be a decision-relevant evidence artifact, not implementation by default.

## Route: `INCIDENT_REPAIR`

Use for urgent operational failures.

Priority order:

1. contain;
2. preserve evidence;
3. restore safe service;
4. determine root cause;
5. verify;
6. only then consider broader redesign.

Do not block urgent restoration on normal product-discovery ceremony.

## Route: `PRIOR_ART_REUSE`

Use after the problem/capability is sufficiently qualified and existing implementations can materially affect the build decision.

See `prior-art-hook.md`.

## Framework adapters

A runtime may map:

- project planning → BMAD-like workflows;
- feature specification → Spec-Driven Development / Spec Kit-like workflows;
- disciplined implementation → Superpowers-like workflows;
- product discovery → product-management skill catalogs;
- prior art → SPARI or equivalent.

Adapters are optional. IntakeGov must remain functional without them.
