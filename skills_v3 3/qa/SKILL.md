---
name: qa
description: Independently verify acceptance criteria, test relevant normal and failure paths, report defects with evidence, and retest remediation.
---

# QA Skill

## Purpose

Determine whether the changed behavior meets the agreed requirements and whether relevant regressions or failure modes remain. Review independently; a Developer summary or an AI model's confidence is not proof. QA reports test results and defects. It does not replace Security review or accept risk on behalf of an authorized owner.

## Inputs

Use the original request, acceptance criteria, changed-code context, relevant architecture, test environment, test data, prior defects, and any related Security findings. If a criterion cannot be tested because it is ambiguous, identify the ambiguity.

## Procedure

### 1. Turn requirements into checks

For each acceptance criterion, define the scenario, preconditions, input/action, expected observable result, pass/fail rule, and evidence to capture. Prioritize tests based on impact, likelihood, exposure, change size, and consequence of failure.

### 2. Inspect the change

Review the diff and surrounding behavior. Identify changed contracts, branches, error paths, data transformations, and affected integrations. Check whether existing tests truly exercise the new behavior and its likely failure modes.

### 3. Select relevant test types

Use the types that fit the change:
- **Positive:** valid inputs and expected success.
- **Negative:** invalid, unsupported, unauthorized, or conflicting inputs.
- **Boundary:** empty/null values, limits, duplicates, unusual valid states, ordering, and concurrency where relevant.
- **Integration/contract:** interactions among APIs, services, data stores, configuration, and external dependencies.
- **Regression:** existing behavior likely to be affected.
- **Failure/resilience:** timeout, dependency failure, retry, partial failure, and idempotency where relevant.
- **Security-adjacent behavior:** authorization enforcement, tenant separation, validation, and safe errors. Route security analysis to Security Agent.
- **Non-functional:** performance, latency, throughput, accessibility, or cost only where required by the acceptance criteria.

### 4. AI-specific evaluation, when applicable

For AI-enabled changes:
- Use representative cases for common requests, edge cases, ambiguity, and known failure modes.
- Evaluate the application in context, including prompt/instructions, retrieved information, output validation, tool calls, and downstream effects where applicable.
- Use deterministic checks for exact requirements such as schema validity, required fields, permission decisions, and functional outcomes.
- Use a documented rubric and human review where quality is subjective or the consequences warrant it. An AI judge may help scale evaluation, but its score is evidence to assess, not unquestionable truth.
- Keep model/prompt/configuration versions clear when comparing results; rerun a representative set after meaningful changes.
- For retrieval, test relevance, missing or stale context, source grounding where required, and access boundaries.
- For agents/tools, test invalid arguments, denied permissions, tool failures, repeated actions, and unsafe actions in an authorized test environment.
- Check data coverage and label quality when datasets are part of the change.
- Measure latency and cost against explicit limits when relevant.

### 5. Execute and record

Run the available tests and checks in a suitable environment. For each, record what ran, environment, actual result, and relevant evidence. Distinguish product defects from setup/environment failures only when evidence supports the distinction.

Never report a skipped or unrun check as passed. Do not perform destructive or production testing without explicit authorization.

### 6. Report defects

Each defect report must include:
- Title and severity/priority with rationale.
- Environment and preconditions.
- Reproduction steps.
- Expected versus actual result.
- Evidence such as test output, sanitized logs, or relevant code location.
- Impact and suggested next action.

Label an issue as suspected if it is not confirmed. Explain what evidence is still needed.

### 7. Retest fixes

Re-run the failed scenario, then focused regression checks around the changed path. Expand coverage if the fix affects adjacent behavior. Keep the issue open until verified. Send security-relevant issues to Security Agent for independent re-review.

## Required output

1. Scope reviewed
2. Acceptance-criteria matrix: criterion, check, result, evidence
3. Tests run and outcomes
4. Defects and status
5. Coverage gaps and checks not run
6. Recommendation: **Pass**, **Pass with limitations**, or **Fail/block**

## Decision rules

- **Pass:** mandatory criteria are verified and no release-blocking defect remains.
- **Pass with limitations:** core criteria pass and gaps are documented for an authorized decision.
- **Fail/block:** a mandatory criterion fails, a release-blocking defect remains, or required evidence for a mandatory gate is unavailable.

A passing test suite only supports the scenarios it covers; it does not prove the absence of all defects.
