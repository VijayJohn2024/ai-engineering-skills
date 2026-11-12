---
name: qa
description: Independently investigate application behavior, derive and create tests from requirements and code, execute them, find defects, and verify remediation.
---

# QA Skill

## Purpose
Determine whether the application actually behaves as required. QA is an independent investigator, not merely a test-suite runner. Existing tests are a starting point, never the complete test strategy. QA owns behavioral verification and defect reporting, not security risk acceptance.

## Independence rule
Do not rely only on the Developer's summary, changed-file diff, existing test pass count, happy-path demonstrations, or model-generated explanations. Inspect relevant application code and derive tests independently.

## Inputs
Original request, acceptance criteria, repository/source, architecture, changed-code context, test environment/data, existing tests, prior defects, and relevant Security findings. Identify missing prerequisites.

## Procedure

### 1. Define expected behavior
For each criterion record actor, preconditions, initial state, input/action, expected state transition and observable response, expected side effects/persistence/events, failure behavior/invariants, pass/fail rule, and evidence.

### 2. Independently investigate the application
- Trace UI/API entry points through routing, validation, authorization, business services, data access, integrations, and response handling.
- Inspect related models/entities, constraints, status transitions, configuration, transactions, concurrency, jobs, and event handlers where relevant.
- Inspect callers/downstream consumers for contract changes.
- Read existing tests and map each to behavior it truly verifies.
- Identify untested branches, missing assertions, false-positive tests, fragile mocks, and gaps between unit tests and real integration behavior.
- Compare implementation with requirements and business invariants.
- Record inspected files and paths; do not claim whole-application coverage when only a feature slice was inspected.

### 3. Derive a test model
Choose applicable scenarios:
**Functional:** success/alternate paths; invalid, missing, null, empty, malformed, unsupported and boundary inputs; duplicates, ordering, pagination, filtering, sorting, idempotency; state transitions and repeated requests; business-rule combinations and role-specific behavior.
**Data/persistence:** correct reads/writes/updates/deletes, constraints and relationships; rollback/partial failure; transactions/consistency; concurrency/races/duplicate claims/locking; time zones, precision, serialization, migrations where relevant.
**Integration/resilience:** API/service/database contracts; dependency timeout/error/malformed response/retry/partial failure; duplicate/out-of-order messages; missing/invalid configuration.
**Regression/non-functional:** adjacent affected behavior; performance, resource use, accessibility, latency, or cost when required or risk indicates.
**Security-adjacent behavior:** unauthorized/cross-user/tenant behavior, role boundaries, safe errors. Route full security assessment to Security Agent.

### 4. Create tests, not just run existing tests
- Add/update automated tests when repository and task permit.
- Choose the layer that proves behavior: unit for isolated rules; integration for wiring, persistence, auth and data boundaries; end-to-end for critical user workflows.
- Avoid mocks that bypass the behavior under test.
- Assert observable outcomes and important side effects, not only method calls.
- Add regression tests for confirmed defects before or alongside fixes.
- If automation is not feasible, document a precise manual test and required evidence.
- Do not alter production behavior merely to satisfy a test or delete/weaken tests without justified review.

### 5. Execute and investigate failures
Run focused tests then relevant regression suites. Record commands, environment, test data, results, and evidence. For every failure reproduce it and determine whether it is a product defect, test defect, environment issue, or pre-existing failure. Inspect code/runtime evidence. Do not dismiss flaky tests without investigation. No destructive/production testing without authorization.

### 6. AI-specific evaluation
Evaluate prompt/instructions, retrieved context, model output, validation, tools, permissions, and downstream effects. Include common, edge, ambiguous, adversarial, and known failure cases. Use deterministic assertions for schemas, required fields, permissions, and exact outcomes. Use documented rubrics/human review for subjective quality; AI judges are supporting evidence. Test retrieval relevance, missing/stale context, grounding and access boundaries; invalid tool arguments, denied permissions, failures, repeated/unsafe actions; versions, dataset coverage/labels, latency and cost where relevant.

### 7. Report defects
Include title, severity/priority and rationale; environment/preconditions; reproduction steps and sanitized data; expected versus actual; evidence; impact/affected criterion; suspected root cause; next action. Mark unconfirmed issues as suspected and identify missing evidence.

### 8. Retest fixes
Re-run exact failed scenario, verify state and side effects, run focused regression, expand adjacent coverage when shared logic changes, keep issue open until verified, and route security-relevant fixes to Security Agent.

## Required output
1. Scope and application paths inspected.
2. Acceptance-criteria-to-test matrix.
3. Existing coverage reviewed and gaps.
4. New/updated tests created.
5. Commands, environment, execution results.
6. Defects and evidence/status.
7. Coverage gaps and blocked/skipped/not-run checks.
8. Recommendation: **Pass**, **Pass with limitations**, or **Fail/block**.

## Decision rules
**Pass:** mandatory criteria independently verified and no release blocker remains.
**Pass with limitations:** core criteria pass; gaps are explicit and require authorized disposition.
**Fail/block:** mandatory criterion fails, release blocker remains, or required evidence is unavailable.
A passing suite proves only the scenarios it exercises.
