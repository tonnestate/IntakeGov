# Runtime Integration

A normal skill cannot guarantee that an agent runtime will load it for every relevant request.

For deterministic "always-first" behavior, install a small global rule in the agent/runtime instructions.

Recommended rule:

> Before executing any request that could create, change, investigate, extend, replace, release, or substantially modify a product, project, system, application, feature, integration, workflow, repository, or reusable artifact, invoke `intake-gov`. Do not begin substantial execution until IntakeGov returns a direct or routed execution state.

Do not force IntakeGov ceremony onto ordinary factual questions or simple conversational requests.

## Existing project context

Where the runtime supports project/workspace memory, give IntakeGov read access to:

- project identity;
- repository/workspace metadata;
- current architecture;
- existing decisions;
- open work;
- constraints;
- approved dependencies;
- previous license/provenance decisions.

Read access for classification should not imply write authority.

## Downstream adapters

A runtime may bind IntakeGov routes to installed methods.

Example mapping:

- `PROJECT_PLANNING` → BMAD or internal project workflow;
- `FEATURE_SPECIFICATION` → Spec Kit/spec-driven workflow;
- `EXISTING_PROJECT_CHANGE` → disciplined engineering workflow;
- `PRODUCT_DISCOVERY` → PM/research skills;
- `PRIOR_ART_REUSE` → SPARI;
- license check → dedicated license/provenance skill or service.

IntakeGov should route by capability, not by brand name.
