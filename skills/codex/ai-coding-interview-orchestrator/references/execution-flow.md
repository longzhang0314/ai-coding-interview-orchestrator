# Execution Flow

This is the full operating loop. Use it when the task is large or the agent seems to be jumping into code too quickly.

## Phase 1: Capture

Inputs can be screenshots, README text, code snippets, or an existing repository.

Actions:

- Extract visible requirements from the prompt.
- Search files with `rg --files`.
- Read README, package/build config, tests, and obvious entry points.
- Note time pressure and avoid broad exploration.

Output:

- Problem restatement
- Known resources
- Missing details

## Phase 2: Decide Scope

Classify requirements:

- P0: required for the system to work
- P1: important quality or usability
- P2: nice-to-have

In interviews, implement P0 first and only then P1.

## Phase 3: Build Spec

Write a compact spec from `spec-template.md`. Keep it executable and implementation-shaped.

## Phase 4: Plan Files

For each file:

- Why it changes
- Main functions/classes
- Test impact

Avoid touching unrelated files.

## Phase 5: Implement

Rules:

- Follow existing style.
- Prefer simple data structures over frameworks when time is short.
- Add abstractions only when the requirement demands extension points.
- Keep AI integrations behind an interface if real credentials are not available.

## Phase 6: Verify

Use `verification-checklist.md`. If tests fail, debug systematically:

- Read exact error.
- Form one hypothesis.
- Make one targeted change.
- Re-run the smallest relevant command.

## Phase 7: Report

Use `final-report-template.md`. Keep it concise enough for an interviewer to scan.
