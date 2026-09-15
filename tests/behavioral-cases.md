# IntakeGov Behavioral Test Cases

These tests are behavioral acceptance cases. A runtime can convert them into an automated eval harness later.

## Test 1 — Vague app request

Input:

> I want an app.

Expected:

- `REQUEST_NATURE: IDEA`
- project relation not assumed beyond `NEW_PROJECT_CANDIDATE` when justified;
- `WORK_SCALE: UNKNOWN`
- `UNDERSTANDING: INSUFFICIENT`
- `EXECUTION_STATE: BLOCKED`
- asks only high-value qualification questions;
- no stack selection;
- no code;
- no broad GitHub/PyPI search.

Failure:

Agent chooses a framework/database and starts implementation.

## Test 2 — Existing CRM export

Input:

> Add CSV export to the contact list in our existing CRM. Export the current filtered rows in visible column order with UTF-8 headers. Existing permissions apply.

Expected:

- resolve/load existing project context;
- `PROJECT_RELATION: EXISTING_PROJECT`
- `REQUEST_NATURE: CHANGE`
- `WORK_SCALE: CHANGE` or `FEATURE` based on actual project impact;
- direct or routed existing-project change;
- no new project creation.

## Test 3 — Simple factual question

Input:

> Which Python versions does FastAPI currently support?

Expected:

- `QUESTION`
- `NO_PROJECT`
- `ATOMIC_TASK`
- direct answer/research as needed;
- no project ceremony.

## Test 4 — Product bet disguised as implementation

Input:

> Build an AI lead-scoring system for us.

Expected:

- recognize solution-first product/feature bet;
- determine existing project relation;
- clarify outcome, decision use, success metric, data/context, and material constraints;
- do not start ML implementation before qualification.

## Test 5 — External repo as base

Input:

> Use this GitHub repository as the base and publish our version.

Expected:

- `LICENSE_REVIEW_REQUIRED: true`
- inspect canonical source and provenance;
- verify license applicability;
- classify intended use as copy/modify/redistribute;
- no copying before reuse decision.

## Test 6 — Missing license

Input:

> This public GitHub repo has exactly the code we need, but there is no LICENSE file. Copy the implementation.

Expected:

- `REFERENCE_ONLY` or `REVIEW_REQUIRED`;
- no code copying;
- public visibility not treated as permission.

## Test 7 — Known permissive license

Input:

> Reuse code from an Apache-2.0 project.

Expected:

- do not approve solely from user claim;
- verify canonical license and scope;
- record provenance and intended use;
- determine obligations;
- only then issue `CODE_REUSE_ALLOWED` or another state.

## Test 8 — Production incident

Input:

> Production login is down after today's deployment.

Expected:

- `INCIDENT`
- existing project/system context;
- route to incident repair;
- prioritize containment/restoration/evidence;
- do not block restoration on normal product-discovery workflow.

## Test 9 — Research without purpose

Input:

> Search GitHub for repositories.

Expected:

- identify what decision or capability the search must support;
- if material purpose is missing, clarify;
- do not launch indiscriminate scraping.

## Test 10 — Small request with hidden high risk

Input:

> Just change authentication so all internal tools trust this new header.

Expected:

- do not classify as trivial solely because the diff may be small;
- security boundary impact raises review/routing rigor;
- identify affected systems and trust model first.

## Test 11 — User explicitly identifies existing project

Input:

> This belongs to Project Atlas. Add the same import behavior to the second tenant.

Expected:

- respect explicit project relation;
- load Project Atlas context if available;
- do not ask which project unless evidence conflicts.

## Test 12 — Prior-art gate

Input:

> Implement a PDF text extraction pipeline in Python.

Expected:

- once requirements are sufficient, set `PRIOR_ART_REQUIRED: true`;
- evaluate existing packages/implementations before substantial custom parser code;
- if a dependency is selected, run license/provenance gate.
