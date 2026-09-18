# AI-Assisted Engineering Roadmap

A practical progression for engineers building software with AI coding agents such as **Claude** or **Codex**.

The goal is to move from:

> **AI-assisted coding → agentic development → automated verification → staging → live testing → production → increasingly autonomous engineering workflows**

The central idea is simple:

> **Don't just make the AI write code. Build a system where the AI can make changes, verify them, observe the results, and iterate safely.**

---

## Roadmap

```text
1. Prompting
      ↓
2. Repository Context
      ↓
3. Delegation
      ↓
4. Verification
      ↓
5. Agentic Development
      ↓
6. Multi-Step Feature Execution
      ↓
7. CI/CD
      ↓
8. Staging Deployment
      ↓
9. Live Testing
      ↓
10. Production Deployment
      ↓
11. Production Feedback
      ↓
12. Increasing Autonomy
```

---

# 1. Prompting — Basic AI-Assisted Coding

### Goal

Learn how to use Claude/Codex effectively for individual engineering tasks.

### Skills

* Give the model a well-scoped coding task.
* Provide the relevant context.
* Ask it to inspect existing code before making changes.
* Ask for an implementation plan before modifying complex code.
* Understand context windows and instruction hierarchy.
* Understand the difference between chat-based assistance and agentic coding.
* Review every generated diff.
* Learn when the model needs more context.
* Learn when the task should be broken into smaller tasks.

### Example

```text
Investigate the authentication middleware.

Before changing anything:

1. Explain how authentication currently works.
2. Identify where tokens are validated.
3. Identify existing tests.
4. Identify any security-sensitive areas.
5. Propose the smallest change necessary.

Do not modify code yet.
```

Then:

```text
Implement the proposed change.

Requirements:

- Follow existing project patterns.
- Add regression tests.
- Run the relevant test suite.
- Run typechecking/linting.
- Show me the final diff.
- Explain anything that remains uncertain.
```

### Milestone

> You can use an AI coding agent to accelerate normal development without losing control of the codebase.

---

# 2. Repository Context — Make the Agent Understand the Codebase

### Goal

Move from isolated prompts to repository-level development.

The agent should understand:

* project structure
* architecture
* coding conventions
* testing conventions
* deployment process
* important constraints
* common commands
* security requirements
* architectural decisions

### Establish Agent Instructions

Depending on the tool, maintain repository-level instructions such as:

```text
CLAUDE.md
AGENTS.md
README.md
docs/
```

These should explain things like:

```text
# Development Guidelines

## Architecture

Describe the major components.

## Commands

Install:
...

Development:
...

Tests:
...

Lint:
...

Typecheck:
...

Build:
...

## Code Style

Describe project conventions.

## Testing

Every new feature should include tests.

## Database

Describe migration requirements.

## Deployment

Describe how deployments work.

## Security

Describe sensitive areas and prohibited behavior.

## Important Constraints

List architectural and product constraints.
```

### Milestone

> The agent can navigate the repository and follow existing engineering conventions without requiring you to explain the same context repeatedly.

---

# 3. Delegation — Give the Agent Real Engineering Tasks

### Goal

Move from asking for code snippets to delegating complete, bounded tasks.

Instead of:

```text
Write a function that validates JWTs.
```

Give it:

```text
Investigate issue #142.

Determine the root cause.

Then:

1. Identify the affected code.
2. Explain the current behavior.
3. Propose a fix.
4. Implement the fix.
5. Add regression tests.
6. Run the relevant tests.
7. Run typechecking and linting.
8. Review the final diff.
9. Report what changed and any remaining risks.

Do not modify unrelated code.
```

### Important Skill

Learn to define:

* objective
* scope
* constraints
* acceptance criteria
* verification steps
* stopping conditions

### Milestone

> You can hand the agent a meaningful engineering task and receive a verified implementation rather than merely generated code.

---

# 4. Verification — Build the Feedback Loop

This is one of the most important milestones.

The AI should not simply generate code and declare success.

Build a loop:

```text
Specification
      ↓
Implementation
      ↓
Test
      ↓
Failure?
   ↙     ↘
 YES      NO
 ↓         ↓
Diagnose   Review
 ↓         ↓
Fix       Complete
 ↓
Test Again
```

### Give the Agent Objective Feedback

The agent should be able to run:

* unit tests
* integration tests
* end-to-end tests
* typechecking
* linting
* formatting
* builds
* security checks
* static analysis

### Example

```text
Implement this feature.

You are not finished when the code compiles.

You are finished only when:

- acceptance criteria are satisfied
- relevant tests pass
- regression tests exist
- typechecking passes
- linting passes
- build succeeds
- final diff has been reviewed
```

### Milestone

> The agent's output is judged by objective verification signals rather than by whether the generated code merely looks plausible.

---

# 5. Agentic Development — Give the AI Tools

Now stop treating Claude/Codex purely as autocomplete.

Start treating it as an **engineering agent**.

Give the agent controlled access to tools such as:

```text
Terminal
Git
Test runner
Build system
Documentation
Issue tracker
Local services
Browser
Database sandbox
API clients
Logs
```

The agent should be able to:

```text
Inspect
   ↓
Plan
   ↓
Modify
   ↓
Run
   ↓
Observe
   ↓
Diagnose
   ↓
Modify
   ↓
Verify
```

### Example Task

```text
Investigate why users are occasionally receiving a 500
when submitting the checkout form.

You may:

- inspect the repository
- search logs
- run the application locally
- reproduce the issue
- inspect database state
- modify code
- add tests

Do not make unrelated changes.

Continue until you have:

1. Identified the root cause.
2. Implemented a fix.
3. Added a regression test.
4. Verified the fix.
5. Summarized the evidence.
```

### Milestone

> The agent can investigate, modify, execute, and verify software rather than simply generate text or code.

---

# 6. Multi-Step Feature Execution

### Goal

Move from individual tasks to complete feature development.

The workflow becomes:

```text
Product Requirement
        ↓
Technical Design
        ↓
Task Decomposition
        ↓
Implementation
        ↓
Testing
        ↓
Pull Request
        ↓
Review
        ↓
Deployment
```

### The Critical Skill: Task Decomposition

Large requests should be broken into independently verifiable pieces.

For example:

```text
Feature: Add organization invitations

1. Design database changes
2. Add invitation model
3. Add migration
4. Add invitation service
5. Add API endpoint
6. Add email integration
7. Add frontend UI
8. Add authorization checks
9. Add unit tests
10. Add integration tests
11. Add end-to-end tests
12. Update documentation
13. Deploy to staging
14. Run smoke tests
```

Each step should have clear acceptance criteria.

### Milestone

> You can give an AI agent a meaningful feature and have it execute the work as a sequence of independently verifiable engineering tasks.

---

# 7. CI/CD — Automate the Quality Gates

The next step is to make verification automatic.

A typical pipeline:

```text
Pull Request
     ↓
Build
     ↓
Typecheck
     ↓
Lint
     ↓
Unit Tests
     ↓
Integration Tests
     ↓
Security Checks
     ↓
AI-Assisted Review
     ↓
Human Review
     ↓
Merge
```

### Example CI Requirements

Every pull request should automatically run:

```text
✓ Build
✓ Typecheck
✓ Lint
✓ Unit tests
✓ Integration tests
✓ Security checks
✓ Migration validation
✓ Dependency checks
```

### AI's Role

The AI can:

* inspect CI failures
* diagnose errors
* propose fixes
* implement fixes
* add missing tests
* review diffs
* explain failures

But the CI system remains an independent verification mechanism.

### Milestone

> AI-generated code is subjected to the same automated quality gates as human-written code.

---

# 8. Staging Deployment

Now connect the development loop to a real environment.

```text
Agent
  ↓
Git Branch
  ↓
Pull Request
  ↓
CI
  ↓
Staging Deployment
  ↓
Automated Tests
  ↓
Smoke Tests
  ↓
Validation
```

The agent should be able to help inspect:

* deployment output
* application logs
* database migrations
* API responses
* frontend behavior
* configuration
* runtime errors
* performance regressions

### Example

```text
Deploy this branch to staging.

After deployment:

1. Verify the deployment succeeded.
2. Check application health.
3. Run the authentication flow.
4. Create a test account.
5. Exercise the new feature.
6. Check application logs.
7. Check browser console errors.
8. Verify database changes.
9. Report any failures.
```

### Milestone

> The agent can help validate software in an environment that resembles production.

---

# 9. Live Testing — Let the Agent Exercise the Software

This is another major transition.

The agent should no longer reason only from source code.

It should be able to interact with the actual running application.

### Tools

Depending on your system:

* Browser automation
* API clients
* End-to-end tests
* Screenshots
* Video capture
* Network inspection
* Browser console
* Application logs
* Error tracking
* Performance monitoring

### Example Web Workflow

```text
Implement
    ↓
Deploy Preview
    ↓
Open Application
    ↓
Execute User Flow
    ↓
Observe Result
    ↓
Inspect Console
    ↓
Inspect Network
    ↓
Inspect Logs
    ↓
Identify Failure
    ↓
Fix
    ↓
Deploy Again
    ↓
Repeat
```

### Example

```text
Test the checkout flow in the deployed staging environment.

Use a test account.

Verify:

1. User can add a product.
2. Cart updates correctly.
3. Checkout page loads.
4. Validation works.
5. Payment test flow completes.
6. Confirmation page appears.
7. Database reflects the order.
8. No browser console errors occur.
9. No server errors occur.

If anything fails, investigate and fix it.
```

### Milestone

> The agent can test the actual running software instead of merely reasoning about whether the code should work.

---

# 10. Production Deployment

Once staging is reliable, introduce production.

The important concept is **controlled autonomy**.

A progression can look like:

```text
Level 1
Agent writes code
Human deploys

        ↓

Level 2
Agent opens PR
CI validates
Human approves

        ↓

Level 3
Agent can deploy to staging automatically

        ↓

Level 4
Agent can deploy bounded, low-risk changes
behind feature flags

        ↓

Level 5
Agent participates in production monitoring
and rollback workflows
```

### Required Infrastructure

Before increasing deployment autonomy, establish:

```text
Feature flags
Automated rollback
Health checks
Monitoring
Alerting
Audit logs
Deployment history
Database backup/recovery
Environment isolation
Secrets management
Access controls
```

### Milestone

> The agent can participate in deployment workflows while the system has strong controls for detecting and reversing failures.

---

# 11. Production Feedback Loop

Eventually production itself becomes part of the engineering loop.

```text
                    ┌──────────────┐
                    │    Users     │
                    └──────┬───────┘
                           ↓
                    ┌──────────────┐
                    │  Production  │
                    └──────┬───────┘
                           ↓
                ┌─────────────────────┐
                │ Logs / Metrics /    │
                │ Traces / Errors     │
                └──────────┬──────────┘
                           ↓
                    ┌──────────────┐
                    │     Agent    │
                    └──────┬───────┘
                           ↓
                  Diagnose / Propose
                           ↓
                    ┌──────────────┐
                    │    Tests     │
                    └──────┬───────┘
                           ↓
                           PR
                           ↓
                       Deployment
                           ↓
                           ↺
```

### Production Signals

Feed useful signals back into engineering:

* error rates
* logs
* traces
* latency
* failed requests
* crash reports
* user-reported bugs
* failed jobs
* queue depth
* database metrics
* infrastructure alerts
* product analytics

### Milestone

> Production behavior can automatically generate actionable engineering work.

---

# 12. Increasing Autonomy

The final milestone isn't simply "let the AI do everything."

Instead, increase autonomy where:

```text
Risk is low
      +
Verification is strong
      +
Observability is strong
      +
Rollback is easy
      =
Higher agent autonomy
```

### Example Autonomy Model

| Level | Agent Capability                     |
| ----- | ------------------------------------ |
| 0     | Generate code                        |
| 1     | Modify code                          |
| 2     | Run tests                            |
| 3     | Debug failures                       |
| 4     | Open PRs                             |
| 5     | Complete multi-step features         |
| 6     | Deploy to staging                    |
| 7     | Perform live tests                   |
| 8     | Diagnose production issues           |
| 9     | Prepare production fixes             |
| 10    | Execute bounded production workflows |

The exact boundaries should depend on the risk of the system.

---

# The Complete Engineering Loop

The mature system looks like this:

```text
                    ┌──────────────────┐
                    │ Product / Issue  │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │ Agent investigates│
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │ Plan / Decompose │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │    Implement     │
                    └────────┬─────────┘
                             ↓
                    ┌──────────────────┐
                    │      Test        │
                    └────────┬─────────┘
                             ↓
                     ┌───────┴────────┐
                     │                │
                   FAIL             PASS
                     │                │
                     ↓                ↓
                  Diagnose          Review
                     │                │
                     ↓                ↓
                   Fix              PR
                     │                │
                     └───────┐        ↓
                             │    CI/CD
                             │        ↓
                             │    Staging
                             │        ↓
                             │  Live Testing
                             │        ↓
                             │   Production
                             │        ↓
                             │ Observability
                             │        ↓
                             └────────↺
```

---

# What You Should Actually Learn

The progression isn't primarily about learning increasingly clever prompts.

It's about developing these engineering capabilities:

## 1. Context Engineering

Learn how to give an agent the information it needs.

```text
Repository
Architecture
Requirements
Constraints
Examples
Documentation
Tests
Runtime information
```

---

## 2. Task Decomposition

Learn how to transform:

```text
"Build this feature"
```

into:

```text
Requirements
→ Design
→ Tasks
→ Implementation
→ Tests
→ Deployment
→ Validation
```

---

## 3. Verification Engineering

Learn how to create objective signals that tell the agent whether it succeeded.

```text
Tests
Typechecking
Linting
Builds
Assertions
Smoke tests
E2E tests
Runtime checks
Monitoring
```

---

## 4. Tool Integration

Give agents access to the systems they need to perform engineering work.

```text
Git
Terminal
CI
Issue tracker
Browser
APIs
Databases
Logs
Monitoring
Cloud infrastructure
```

---

## 5. Observability

The agent needs to see what happened after its changes.

```text
Logs
Metrics
Traces
Errors
Screenshots
Test results
Runtime state
```

Without observability, an agent is forced to guess.

---

## 6. Safe Autonomy

Autonomy should be earned through verification.

```text
More autonomy
      ↑
      │
Better verification
      │
Better observability
      │
Better rollback
      │
Better isolation
      │
Better tests
```

---

# Practical Milestone Checklist

Use this as a personal progression checklist.

## Level 1 — AI Coding

* [ ] I can effectively delegate small coding tasks.
* [ ] I understand how to provide useful context.
* [ ] I review generated diffs.
* [ ] I know when to ask for a plan first.
* [ ] I can recognize when an agent lacks necessary context.

## Level 2 — Repository Agent

* [ ] My repository has clear development instructions.
* [ ] The agent understands project conventions.
* [ ] The agent can navigate the repository.
* [ ] The agent can run the project's standard commands.
* [ ] The agent can find relevant tests.

## Level 3 — Delegated Engineering

* [ ] I can give the agent complete issues.
* [ ] Issues have clear acceptance criteria.
* [ ] Tasks have explicit scope.
* [ ] The agent can implement changes independently.
* [ ] The agent reports what it changed.

## Level 4 — Verification

* [ ] Tests are automated.
* [ ] Typechecking is automated.
* [ ] Linting is automated.
* [ ] Builds are automated.
* [ ] Regression tests are expected.
* [ ] Agents must verify their own work.

## Level 5 — Agentic Development

* [ ] The agent can use the terminal.
* [ ] The agent can use Git.
* [ ] The agent can run tests.
* [ ] The agent can diagnose failures.
* [ ] The agent can iterate without constant intervention.

## Level 6 — Feature Execution

* [ ] The agent can decompose features.
* [ ] The agent can execute multiple related tasks.
* [ ] Each task has verification criteria.
* [ ] The agent can prepare a complete PR.
* [ ] The agent can update documentation.

## Level 7 — CI/CD

* [ ] Every PR runs automated checks.
* [ ] Failed checks provide actionable feedback.
* [ ] Agents can investigate CI failures.
* [ ] Deployment is automated.
* [ ] Changes are auditable.

## Level 8 — Staging

* [ ] Agents can deploy to staging.
* [ ] Health checks exist.
* [ ] Smoke tests exist.
* [ ] Staging resembles production.
* [ ] Agents can inspect staging logs.

## Level 9 — Live Testing

* [ ] Browser/API testing is automated.
* [ ] Agents can exercise deployed applications.
* [ ] Runtime errors are observable.
* [ ] Agents can inspect console/network output.
* [ ] Agents can iterate based on live test results.

## Level 10 — Production

* [ ] Production deployments are controlled.
* [ ] Feature flags exist where appropriate.
* [ ] Rollbacks are automated or well-defined.
* [ ] Monitoring and alerting exist.
* [ ] Deployment history is auditable.

## Level 11 — Production Feedback

* [ ] Production errors create actionable signals.
* [ ] Logs are accessible.
* [ ] Metrics are accessible.
* [ ] Traces are accessible where appropriate.
* [ ] Agents can investigate production issues.
* [ ] Agents can prepare fixes from production evidence.

## Level 12 — Controlled Autonomy

* [ ] Agents can independently execute bounded workflows.
* [ ] High-risk operations require additional approval.
* [ ] Automated verification gates exist.
* [ ] Rollback mechanisms exist.
* [ ] Agent actions are logged.
* [ ] Permissions are scoped to what the agent actually needs.
* [ ] Autonomy increases only when verification and observability support it.

---

# The Core Principle

The evolution looks like this:

```text
AI writes code
      ↓
AI understands repository
      ↓
AI executes tasks
      ↓
AI runs tests
      ↓
AI debugs failures
      ↓
AI completes features
      ↓
AI opens PRs
      ↓
AI deploys to staging
      ↓
AI tests the running application
      ↓
AI participates in deployment
      ↓
AI observes production
      ↓
AI helps diagnose production issues
      ↓
AI executes bounded engineering workflows
```

The ultimate goal is not:

> **"Make AI write more code."**

It is:

> **"Build an engineering environment in which AI can safely execute more of the software-development loop."**

The most important infrastructure isn't the prompt.

It's the combination of:

```text
Context
+
Tools
+
Tests
+
CI/CD
+
Staging
+
Live Testing
+
Observability
+
Rollback
+
Access Controls
+
Human Oversight
```

Together, these turn an AI coding assistant into a progressively more capable engineering system.
