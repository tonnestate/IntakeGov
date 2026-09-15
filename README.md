# IntakeGov

**Classify before you execute.**

IntakeGov is an open Agent Skill for project and product intake governance.

It treats substantive requests as unclassified work until an agent determines:

- what kind of request it is;
- whether it belongs to an existing project, a new project candidate, or no project;
- whether the request is sufficiently understood for its next stage;
- how large/risky the work is;
- which delivery workflow should handle it;
- whether prior-art evaluation is required;
- whether external artifacts require a license/provenance gate.

The goal is to prevent AI agents from prematurely turning vague intent into architecture and code.

## Status

`0.1.0` — initial behavioral specification.

The first version is intentionally a skill and reference model, not an orchestration server.

## Design principles

- qualification before implementation;
- existing context before greenfield assumptions;
- minimal, decision-relevant clarification;
- proportional process;
- prior art before unnecessary custom builds;
- fail-closed license/provenance handling;
- framework-neutral routing;
- explicit behavioral tests.

## Repository structure

```text
intake-gov/
├── SKILL.md
├── LICENSE
├── NOTICE
├── THIRD_PARTY_NOTICES.md
├── README.md
├── CHANGELOG.md
├── references/
│   ├── qualification-model.md
│   ├── work-classification.md
│   ├── routing-model.md
│   ├── license-provenance-gate.md
│   ├── prior-art-hook.md
│   └── runtime-integration.md
└── tests/
    └── behavioral-cases.md
```

## Installation

Install the `intake-gov` skill folder in a client/runtime that supports Agent Skills or equivalent `SKILL.md` instructions.

For true always-first behavior, also configure the runtime rule in `references/runtime-integration.md`.

## License

Apache-2.0.

## Prior art

IntakeGov is independently written. Its design was informed by public software-delivery and product-management projects listed in `THIRD_PARTY_NOTICES.md`.

Those projects are references, not bundled dependencies.

## Roadmap

- executable eval harness;
- optional adapters for major delivery frameworks;
- structured intake state schema;
- License & Provenance companion skill;
- SPARI prior-art/reuse companion skill;
- optional MCP/control-plane integration after the skill contracts stabilize.
