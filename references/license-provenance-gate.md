# License & Provenance Gate

This gate applies whenever an external artifact may influence a reusable deliverable.

It is a workflow control, not legal advice.

## Core rule

`NO REUSE WITHOUT VERIFIED LICENSE AND PROVENANCE`

Public availability is not permission.

Repository visibility, package availability, stars, forks, or installation capability do not replace a license.

## Artifacts covered

Apply this gate to:

- source code;
- repositories;
- packages and dependencies;
- code snippets;
- templates;
- agent skills;
- prompts distributed as reusable artifacts;
- documentation;
- datasets;
- models and weights;
- images;
- icons;
- fonts;
- audio/video;
- generated assets with external source material;
- examples;
- vendored files.

## Required checks

### Source

Record the canonical source.

Prefer upstream/original source over mirrors, forks, aggregators, or copied snippets.

### Provenance

Record, where available:

- repository;
- commit SHA;
- tag/release;
- package name/version;
- file path;
- artifact hash;
- publisher/maintainer.

### License identification

Determine:

- license expression;
- authoritative license file;
- whether per-file or directory exceptions exist;
- whether documentation/assets/data use separate licenses;
- whether vendored third-party material has separate terms;
- whether repository metadata conflicts with actual license text.

A repository-level label alone is insufficient when the target artifact has different licensing.

### Intended reuse

Classify the planned use:

- learn/reference;
- pattern abstraction;
- dependency;
- copy;
- modify;
- vendor;
- redistribute;
- embed;
- publish;
- commercial distribution.

### Obligations

Identify requirements relevant to the intended use, such as:

- attribution;
- preservation of notices;
- inclusion of license text;
- NOTICE handling;
- source-disclosure obligations;
- reciprocal/share-alike obligations;
- modification notices;
- patent-related terms;
- network-use conditions;
- restrictions outside standard open-source licenses.

### Compatibility

Determine whether the intended reuse is compatible with the target project's distribution and licensing model.

Do not infer compatibility from both licenses being "open source".

## Decision states

### `REFERENCE_ONLY`

Allowed:

- inspect;
- compare;
- understand behavior;
- learn concepts;
- record source and findings.

Not allowed:

- copy source into the target;
- vendor;
- redistribute;
- create a direct derivative artifact when permission is unclear.

Default for missing or unclear license.

### `PATTERN_ONLY`

The implementation concept or architecture may be used as reference, but source must be independently written.

Use when direct code reuse is unnecessary or undesirable.

### `DEPENDENCY_ALLOWED`

The artifact may be used as a dependency under identified conditions.

Record obligations and version.

### `CODE_REUSE_ALLOWED`

Concrete source may be reused for the stated target/use after obligations are satisfied.

This status is use-specific, not globally transferable.

### `REVIEW_REQUIRED`

Automatic reuse is blocked.

Use for:

- unclear/custom license;
- conflicting license evidence;
- substantial copyleft implications;
- dual-license ambiguity;
- uncertain target compatibility;
- unclear ownership/provenance;
- license exceptions requiring interpretation.

### `DENIED`

The planned reuse is not permitted under current policy or known terms.

## Fail-closed behavior

If any of the following is unresolved, automatic copying/reuse must stop:

- no license;
- unknown license;
- unclear applicability to the target artifact;
- conflicting notices;
- unknown provenance;
- incompatible intended use;
- unmet obligations.

`UNCLEAR` never means `ALLOWED`.

## Persistence

Store license decisions with:

- artifact identity;
- version/commit;
- source;
- license evidence;
- intended reuse;
- decision;
- obligations;
- decision date;
- verification evidence.

Revalidate when the artifact version or source changes materially.

## Relationship to prior-art research

Prior-art systems may freely discover candidates.

Discovery does not grant reuse permission.

License/provenance evaluation occurs before incorporation into a deliverable.
