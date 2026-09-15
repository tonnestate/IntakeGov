# Prior-Art / Reuse Hook

This file defines the contract between IntakeGov and a future software prior-art/reuse system such as SPARI.

IntakeGov decides **when** prior-art evaluation is required.

The prior-art system decides **what already exists and whether it is a sensible base**.

## Preconditions

Do not run broad prior-art discovery from a vague solution request.

The handoff should include:

- qualified outcome;
- capability or problem statement;
- project context;
- constraints;
- success criteria;
- relevant architecture/runtime constraints;
- intended distribution model when reuse may occur.

## Expected prior-art search layers

A mature implementation should consider, when relevant:

1. internal project/codebase exemplars;
2. existing organization components;
3. package registries;
4. source repositories;
5. frameworks/applications;
6. standards/reference implementations;
7. official documentation;
8. web research only as necessary;
9. scraping only as fallback when direct/structured access is unavailable.

## Required candidate decision

Each serious candidate should resolve to one of:

- `ADOPT`
- `ADAPT`
- `COMPOSE`
- `REFERENCE`
- `REJECT`
- `BUILD`

`BUILD` should require evidence that custom implementation is justified relative to viable prior art.

## Required reuse handoff

If a candidate may be incorporated:

- invoke the License & Provenance Gate;
- attach the reuse decision;
- retain source/version evidence;
- do not copy external code before the reuse state permits it.

## Learning loop

A prior-art system should persist:

- capability;
- candidate;
- decision;
- rationale;
- source/version;
- license decision;
- implementation outcome;
- test evidence;
- known limitations;
- last verification date.

Future agents should consult prior decisions before starting the same research again.
