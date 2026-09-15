# IntakeGov

<p align="center">
  <strong>Classify before you execute.</strong><br>
  An always-first project and product intake governor for AI agents.
</p>

<p align="center">
  <img alt="License" src="https://img.shields.io/badge/license-Apache--2.0-blue">
  <img alt="Status" src="https://img.shields.io/badge/status-experimental-orange">
  <img alt="Version" src="https://img.shields.io/badge/version-0.1.0-green">
  <img alt="Agent Skill" src="https://img.shields.io/badge/agent-skill-purple">
</p>

---

## Why IntakeGov exists

AI agents are increasingly good at planning, coding, researching, and executing.

But they still fail surprisingly often at the step that comes **before** all of that:

> **What kind of request is this, does it belong to an existing project, is it sufficiently understood, and what is the correct way to handle it?**

A user says:

> “I want an app.”

And an agent may immediately choose React, FastAPI, PostgreSQL, Docker, and a deployment architecture.

A user says:

> “Add this to our dashboard.”

And the agent may treat it as a new project instead of loading the existing project context.

A user says:

> “Use this GitHub repository as the base.”

And the agent may start copying code without first verifying provenance, license scope, redistribution rights, or compatibility.

A user says:

> “Build a PDF extraction pipeline.”

And the agent may write one from scratch before checking whether a mature package or reference implementation already exists.

**IntakeGov exists to prevent that class of mistake.**

---

## The idea

Every substantive request starts as:

```text
UNCLASSIFIED_WORK
```

Before substantial execution begins, IntakeGov determines:

```text
What is being requested?
        ↓
Does it belong to an existing project?
        ↓
Is the outcome sufficiently understood?
        ↓
What kind of work is this?
        ↓
How large / risky / cross-cutting is it?
        ↓
Which delivery path fits?
        ↓
Is prior-art / reuse research required?
        ↓
Will external artifacts be reused?
        ↓
Is license + provenance review required?
        ↓
Only then:
EXECUTE
```

The goal is not to add bureaucracy.

The goal is to avoid using the **wrong execution model**.

---

## What IntakeGov classifies

### Request nature

```text
QUESTION
ACTION
CHANGE
INVESTIGATION
IDEA
PRODUCT_BET
INCIDENT
UNKNOWN
```

### Project relation

```text
NO_PROJECT
STANDALONE
EXISTING_PROJECT
NEW_PROJECT_CANDIDATE
UNKNOWN
```

### Work scale

```text
ATOMIC_TASK
CHANGE
FEATURE
EPIC
PROJECT
UNKNOWN
```

### Understanding

```text
INSUFFICIENT
SUFFICIENT
```

### Execution state

```text
BLOCKED
DIRECT
ROUTED
```

These dimensions are intentionally separate.

A tiny code change can still be high-risk.  
A long research task is not automatically a project.  
A vague “app idea” is not yet a qualified project.

---

## Example

### Input

```text
I want an app.
```

### IntakeGov

```text
REQUEST_NATURE: IDEA
PROJECT_RELATION: NEW_PROJECT_CANDIDATE
WORK_SCALE: UNKNOWN
UNDERSTANDING: INSUFFICIENT
DELIVERY_READINESS: NOT_READY
EXECUTION_STATE: BLOCKED
```

The agent must clarify the material gaps first.

It must **not** immediately:

- select a stack;
- define an architecture;
- create a repository;
- start broad GitHub research;
- generate substantial implementation code.

---

## Another example

### Input

```text
Add CSV export to the contact list in our existing CRM.
Export the currently filtered rows in visible column order.
UTF-8 with headers. Existing permissions apply.
```

### IntakeGov

```text
REQUEST_NATURE: CHANGE
PROJECT_RELATION: EXISTING_PROJECT
WORK_SCALE: CHANGE or FEATURE
UNDERSTANDING: SUFFICIENT
DELIVERY_READINESS: READY
EXECUTION_STATE: ROUTED
```

The correct next step is to load the existing project context and route the work through a bounded change workflow.

No new project.  
No greenfield architecture.  
No unnecessary ceremony.

---

# Core principles

## 1. Existing context before greenfield assumptions

If a request may belong to an existing project, IntakeGov resolves that context before classifying the work as a new project.

## 2. Clarify only what matters

No generic 20-question intake form.

IntakeGov asks only questions whose answers can materially change:

- project relation;
- scope;
- success criteria;
- architecture;
- risk;
- delivery route;
- licensing;
- feasibility.

## 3. Build is not the default

If mature prior art may materially change the solution, a prior-art / reuse evaluation is required before substantial custom implementation.

## 4. Process must match the work

A simple factual question should not trigger project-management ceremony.

A high-risk or cross-system change should not be treated as an atomic task just because the final diff may be small.

## 5. No external reuse without license and provenance review

Public availability is not permission.

Before external code, packages, repositories, templates, skills, assets, models, datasets, or other artifacts are incorporated into a deliverable, IntakeGov requires an explicit reuse state:

```text
REFERENCE_ONLY
PATTERN_ONLY
DEPENDENCY_ALLOWED
CODE_REUSE_ALLOWED
REVIEW_REQUIRED
DENIED
```

Unknown or missing licensing never silently becomes permission.

---

# Where IntakeGov fits

IntakeGov is **not** intended to replace project-management, product-management, specification, engineering, or research frameworks.

It decides **when they should be used**.

```text
                           ANY REQUEST
                                │
                                ▼
                     ┌─────────────────────┐
                     │      IntakeGov      │
                     │ classify + qualify  │
                     └──────────┬──────────┘
                                │
                ┌───────────────┼────────────────┐
                │               │                │
                ▼               ▼                ▼
           DIRECT ANSWER   EXISTING CHANGE   NEW INITIATIVE
                                │                │
                                ▼                ▼
                         Spec / Engineering   Discovery / PM
                                │                │
                                └───────┬────────┘
                                        ▼
                                  PRIOR ART
                                        │
                                        ▼
                               LICENSE / PROVENANCE
                                        │
                                        ▼
                                   EXECUTION
                                        │
                                        ▼
                                  VERIFICATION
```

A future companion project, **SPARI**, is planned for the prior-art / software-reuse layer.

Its purpose will be to help agents answer:

> What already exists, what is worth reusing, what should only be used as reference, and when is custom implementation actually justified?

---

# License & provenance are first-class

IntakeGov follows a fail-closed rule:

> **No reuse without verified license and provenance.**

For an external artifact, the intended reuse must be evaluated against:

- canonical source;
- version / commit / release;
- applicable license;
- per-file or per-directory exceptions;
- separate asset or documentation licenses;
- intended use;
- redistribution model;
- attribution requirements;
- NOTICE obligations;
- copyleft / reciprocal obligations;
- compatibility with the target project.

A GitHub repository being public does **not** mean its code may be copied.

See:

[`references/license-provenance-gate.md`](references/license-provenance-gate.md)

---

# Routing model

IntakeGov can route work into generic execution modes such as:

- `DIRECT_ANSWER`
- `DIRECT_BOUNDED_EXECUTION`
- `EXISTING_PROJECT_CHANGE`
- `FEATURE_SPECIFICATION`
- `PROJECT_PLANNING`
- `PRODUCT_DISCOVERY`
- `INVESTIGATION`
- `INCIDENT_REPAIR`
- `PRIOR_ART_REUSE`

These are deliberately framework-neutral.

A runtime may map them to BMAD, Spec Kit, Superpowers, internal workflows, or other compatible methods.

---

# Why not just use BMAD, Superpowers, or Spec Kit?

Because those tools become most useful **after the system already understands what kind of work it is dealing with**.

IntakeGov operates one layer earlier.

It answers:

> Is this a question, change, feature, investigation, incident, product bet, epic, or project?

> Does it belong to something that already exists?

> Are the requirements good enough for the next stage?

> Which methodology should handle it?

> Is prior-art evaluation necessary?

> Are we allowed to reuse the external artifacts being considered?

That is the missing decision layer IntakeGov is designed to provide.

---

# Conceptual prior art

IntakeGov is independently written.

Its design was informed by several excellent open-source projects and methodologies. They are **references**, not bundled dependencies, and IntakeGov does not claim affiliation with them.

| Project | License | What informed IntakeGov |
|---|---|---|
| [BMad Method](https://github.com/bmad-code-org/BMAD-METHOD) | MIT | Adaptive planning depth, project/change workflows |
| [Superpowers](https://github.com/obra/superpowers) | MIT | Engineering discipline, workflow gating, behavioral skill testing |
| [specdd](https://github.com/unboundinnov/specdd) | MIT | Triage, targeted clarification, spec-driven progression |
| [GitHub Spec Kit](https://github.com/github/spec-kit) | MIT | Specification, clarification, planning, artifact consistency |
| [GitHub awesome-copilot](https://github.com/github/awesome-copilot) | MIT | Codebase knowledge, architecture and quality workflow patterns |
| [Product on Purpose / pm-skills](https://github.com/product-on-purpose/pm-skills) | Apache-2.0 | Product discovery, build-risk review, lifecycle thinking |

For detailed attribution policy, see:

[`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md)

---

# Repository structure

```text
intake-gov/
├── SKILL.md
├── README.md
├── LICENSE
├── NOTICE
├── THIRD_PARTY_NOTICES.md
├── CHANGELOG.md
│
├── references/
│   ├── qualification-model.md
│   ├── work-classification.md
│   ├── routing-model.md
│   ├── license-provenance-gate.md
│   ├── prior-art-hook.md
│   └── runtime-integration.md
│
└── tests/
    └── behavioral-cases.md
```

---

# Installation

Install the `intake-gov` directory in a runtime that supports Agent Skills or an equivalent `SKILL.md` mechanism.

For deterministic **always-first** behavior, the runtime also needs a small global invocation rule.

Recommended rule:

```text
Before executing any request that could create, change, investigate,
extend, replace, release, or substantially modify a product, project,
system, application, feature, integration, workflow, repository, or
reusable artifact, invoke intake-gov.

Do not begin substantial execution until IntakeGov returns a direct
or routed execution state.
```

See:

[`references/runtime-integration.md`](references/runtime-integration.md)

---

# Behavioral tests

IntakeGov already includes behavioral acceptance cases for scenarios such as:

- vague “I want an app” requests;
- existing-project changes;
- factual questions that should bypass project ceremony;
- product bets disguised as implementation requests;
- reuse of public GitHub repositories;
- missing licenses;
- Apache-2.0 reuse verification;
- production incidents;
- purposeless GitHub research;
- small but security-sensitive changes;
- project-context preservation;
- prior-art evaluation before custom implementation.

See:

[`tests/behavioral-cases.md`](tests/behavioral-cases.md)

---

# Roadmap

## 0.1.x — Intake foundation

- [x] Request classification
- [x] Existing/new project resolution
- [x] Stage-relative requirement qualification
- [x] Proportional routing
- [x] License & provenance gate
- [x] Prior-art handoff contract
- [x] Behavioral test cases

## Next

- [ ] Structured intake state schema
- [ ] Executable eval harness
- [ ] Framework adapters
- [ ] Dedicated License & Provenance companion skill
- [ ] **SPARI** — Software Prior Art & Reuse Intelligence
- [ ] Persistent prior-art / reuse memory
- [ ] Optional MCP/control-plane integration
- [ ] Project lifecycle and post-release learning hooks

---

# The long-term goal

The long-term idea is simple:

> AI agents should not become better only at executing instructions.

They should become better at deciding **what kind of work they are looking at, what already exists, what is actually worth building, what they are allowed to reuse, and which process is appropriate before execution begins.**

IntakeGov is the first layer of that system.

---

## License

Apache License 2.0.

See [`LICENSE`](LICENSE).

---

<p align="center">
  <strong>Understand first. Route correctly. Reuse responsibly. Then execute.</strong>
</p>
