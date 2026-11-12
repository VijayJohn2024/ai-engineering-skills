# Production Engineering Workflow Skills

Version 2.0

This pack defines an evidence-driven workflow for implementation, independent QA, and application-specific security assessment.

## Roles
- **Core Engineering Standards** coordinates scope, acceptance criteria, specialist reviews, findings, remediation, and completion.
- **Developer** investigates and implements the smallest complete solution, adds appropriate tests, verifies changes, and remediates findings.
- **QA** independently investigates application behavior, derives and creates tests, executes them, identifies defects, and verifies fixes.
- **Security Agent** maps the real attack surface and trust boundaries, inspects relevant code paths, validates applicable risks safely, and independently verifies remediation.

## Mandatory workflow
Request → inspect context → define acceptance criteria and verification → plan → implement → developer verification → independent QA → Security review when required → remediate → re-test/re-review → evidence-based completion.

QA is expected for code or behavior changes unless a justified exception (such as documentation-only work) is recorded. Security review is required for security-sensitive changes and when project policy requires it. QA and Security must inspect relevant implementation independently; neither may rely only on the Developer's summary or existing tests.

## Minimum investigation standard
Every role must inspect actual repository/application evidence, trace relevant execution paths, distinguish facts from assumptions, select checks based on actual behavior and risk, capture evidence, and disclose unassessed or blocked areas. Never claim a check passed without observed evidence.

## Learning-material principles operationalized
- Evaluation-driven development and repeatable success/failure cases.
- Whole-application evaluation in context.
- Prompt/model experiments and regression cases when AI is present.
- Retrieval quality, provenance, and access boundaries.
- Application-enforced tool permissions and safe consequential actions.
- Application reconnaissance, architecture and attack-surface analysis.
- Layered security and defense in depth.
- API object-, property-, and function-level authorization.
- Authentication, sessions, injection, browser, XML, dependency, resource, data protection, and operational security.
- Data minimization, key management, monitoring, and incident readiness where applicable.

Apply only relevant controls. PCI DSS concepts do not imply PCI applicability or compliance; check the applicable current standard for formal compliance decisions.

## Versioning and evolution

This repository maintains the engineering skills through incremental improvements.

- **Initial implementation:** Establishes the foundational roles, responsibilities, and engineering workflow.
- **Version 2.0:** Strengthens the initial implementation with deeper application investigation, independent QA validation, application-specific security assessment, and stricter evidence-based completion requirements.

The Git commit history is the source of truth for tracking changes between implementations. Previous implementations remain available through Git history for comparison and reference. The latest committed skill definitions represent the current recommended workflow.

## Using the skills

The Developer, QA, and Security Agent skills can be invoked independently when focused execution is required. Core Engineering Standards acts as the workflow coordinator when a complete, coordinated engineering process is needed; it is not a technical dependency of the other three skills.

For complete feature development, use the coordinated workflow:

Request → Developer → Independent QA → Security review (when required) → Remediation → Revalidation → Completion.

## Execution limitation
A Markdown skill is an instruction set; it does not execute itself. The host platform must load it, invoke the relevant agent, provide repository context and authorized tools, and route findings. If an agent cannot be invoked, mark the review blocked or not performed.

## Status vocabulary
- **Passed**: check ran and met expected result.
- **Failed**: check ran and did not meet expected result.
- **Blocked**: prerequisite prevented execution.
- **Skipped**: intentionally not run, with rationale.
- **Not run**: not executed.
- **Not assessed**: outside the review actually performed.

A passing suite supports only scenarios it covers. “No findings identified in the reviewed scope” is not a guarantee of security.
