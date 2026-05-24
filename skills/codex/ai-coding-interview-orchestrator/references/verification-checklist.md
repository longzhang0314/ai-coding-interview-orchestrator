# Verification Checklist

Run this before claiming the task is complete.

## Repository Basics

- Check current status with `git status` if the repo uses git.
- Identify the real test command from README, package files, build files, or existing CI config.
- If dependencies are missing and network is unavailable, state that clearly and run static or manual checks.

## Minimal Verification Ladder

Use the highest rung available within interview time:

1. Existing test suite passes.
2. New focused tests pass.
3. Smoke command runs the main path.
4. Static syntax/import check passes.
5. Manual sample input produces expected output.

## Bounded Repair Policy

Verification failures must not create an endless repair loop.

- Default repair budget: 2 rounds.
- A repair round starts when code, config, dependency setup, or tests are changed to fix a verification failure.
- After each repair round, re-run the smallest relevant verification command, not the full suite by default.
- If the same failure remains after 2 rounds, stop and report controlled incomplete status.
- If a new unrelated failure appears after a fix, count it as part of the same budget unless the user explicitly expands scope.
- Continue beyond the budget only after explicit user approval.

When the budget is exhausted, produce:

- Checks that passed
- Checks that still fail
- Most likely remaining cause
- Files changed
- Whether the core happy path appears usable
- Suggested next manual decision

## Language Hints

### Python

- `python -m pytest`
- `python -m unittest`
- `python -m py_compile <file.py>`
- Run the CLI/module with a small sample.

### Java / Spring Boot

- `mvn test`
- `mvn -q -DskipTests package`
- Run focused unit tests if the whole suite is slow.
- Check controller/service wiring and configuration names.

### Node / TypeScript

- `npm test`
- `npm run lint`
- `npm run typecheck`
- `npm run build`
- Run the CLI or dev smoke path if tests are absent.

### Frontend

- Build or typecheck first.
- Use browser verification only when the app has a visual workflow and a dev server can run.
- Check responsive layout if UI was changed.

## Final Self-Review

- Did the implementation cover every must-have requirement?
- Are assumptions stated in the final report?
- Are error messages understandable?
- Is there at least one happy-path proof?
- Is there at least one edge-path proof or explanation?
- Did repair stay within the 2-round budget, or did the user approve continuing?
- Are secrets, unsafe eval/deserialization, SQL injection, or path traversal risks addressed when relevant?
