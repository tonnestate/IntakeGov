# Work Classification

Use orthogonal classifications. Do not collapse request type, project relation, and work scale into one label.

## Request nature

### QUESTION

The user primarily wants information or explanation.

### ACTION

A concrete operation with a known target and outcome.

### CHANGE

Modification of an existing artifact, system, product, repository, workflow, or configuration.

### INVESTIGATION

Evidence gathering, diagnosis, comparison, audit, research, spike, or feasibility work.

### IDEA

A proposed solution or opportunity that is not yet sufficiently framed as a product decision.

### PRODUCT_BET

A proposed product/feature investment whose user value or business value must be evaluated.

### INCIDENT

Production breakage, outage, security event, corruption, or urgent operational defect.

### UNKNOWN

The request cannot yet be reliably classified.

## Project relation

### NO_PROJECT

No project context is needed.

### STANDALONE

The work is self-contained and does not need durable project governance.

### EXISTING_PROJECT

The work belongs to an existing project, repository, product, system, or initiative.

### NEW_PROJECT_CANDIDATE

The request plausibly requires a durable new project, but project creation is not final until qualification is sufficient.

### UNKNOWN

Project relation cannot yet be determined.

## Work scale

### ATOMIC_TASK

Single bounded operation with minimal uncertainty and negligible coordination.

Typical characteristics:

- one target;
- one outcome;
- low blast radius;
- no architectural decision;
- no product discovery.

### CHANGE

Bounded change to an existing system.

May require tests and review but not a new specification hierarchy.

### FEATURE

Non-trivial user/system capability with multiple acceptance conditions or components.

Usually requires explicit specification and verification.

### EPIC

Multiple related features or substantial cross-component work sharing one outcome.

Usually requires sequencing and architecture awareness.

### PROJECT

Durable multi-workstream effort with independent planning, multiple features/epics, architecture or delivery coordination, or significant product uncertainty.

## Scale signals

Increase scale when one or more are material:

- multiple subsystems;
- multiple repositories;
- multiple user roles;
- new data model;
- new deployment topology;
- new product surface;
- cross-team coordination;
- migration;
- long-lived state;
- compliance;
- security boundary changes;
- external integrations;
- substantial uncertainty;
- multiple independent releases;
- irreversible or high-blast-radius change.

Do not classify by code size alone.

## False positives to avoid

- A long research answer is not automatically a project.
- A one-line configuration change can still be high-risk.
- A visually small UI change can be a feature when behavior, permissions, or data flows change.
- A prototype can still require project-level discovery when its purpose is unclear.
