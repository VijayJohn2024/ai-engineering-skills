# Engineering Workflow Skills

This pack defines a reusable, evidence-driven workflow for software development. The skills are based on the engineering principles and AI application practices in the provided learning material, expressed as actionable procedures rather than chapter references.

## Roles

- **Core Engineering Standards**: coordinates work, defines success, assigns reviews, routes findings, and decides whether completion criteria have been met.
- **Developer**: investigates and implements changes, verifies them, and fixes reported issues.
- **QA**: independently tests expected behavior, failure paths, edge cases, and regressions; reports evidence and retests fixes.
- **Security Agent**: reviews trust boundaries and security risks; reports evidence-backed findings and verifies security remediation.

## Workflow

Request → inspect context → define observable acceptance criteria and checks → plan → implement → run relevant checks → invoke QA and Security as applicable → fix findings → re-test and re-review → final evidence-based decision.

The Core skill coordinates the workflow. Developer owns implementation. QA owns behavioral verification. Security owns security analysis. No role may claim another role's checks were completed without evidence.

## How the skills relate to the provided learning material

The content is operationalized as practical behavior:
- Define success and build repeatable evaluation before relying on outcomes.
- Evaluate the complete application in its actual context, not just one component in isolation.
- Experiment systematically when adjusting prompts or model behavior.
- Provide relevant context through retrieval when applicable, while treating retrieved content as untrusted.
- Constrain agent tools and consequential actions with application-enforced permissions.
- Choose the simplest technique that addresses the observed problem.
- Consider dataset quality, latency, cost, observability, guardrails, and user feedback when they apply to the system.

These are guiding principles, not mandatory AI checks for every project. AI-specific procedures activate only when the application actually uses models, prompts, retrieval, datasets, or agents.

## Important execution limitation

A Markdown skill is an instruction set; it does not run on its own. The host platform must load the relevant skill, invoke the appropriate agent/role, provide the required repository context and authorized tools, and route findings to the Developer and coordinator. If the platform cannot invoke the Security Agent, the security review must be marked blocked/not performed—not reported as complete.

## Evidence and completion

Record checks as **passed**, **failed**, **blocked**, **skipped**, or **not run**. A recommendation is not proof that a fix works. A passing test suite only provides evidence for the scenarios it covers. “No findings identified in the reviewed scope” is not a guarantee of security.
