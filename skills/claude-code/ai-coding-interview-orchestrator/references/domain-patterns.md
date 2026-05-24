# Domain Patterns For Coding Interviews

Use this file when the business domain is unfamiliar. Convert the problem into a familiar software shape before coding.

## Universal Model

Most interview systems can be reduced to:

- **Input**: file, request, event, command, form, dataset, message
- **Parser**: turns raw input into structured objects
- **Rule/Policy**: decides what is valid, risky, allowed, or recommended
- **Processor**: applies rules and builds results
- **Storage/State**: optional persistence, cache, session, history
- **Output**: report, response, dashboard, exported file, notification
- **Configuration**: thresholds, enabled rules, credentials, modes
- **Errors**: invalid input, missing config, external failure, partial result

## Common Problem Shapes

### Code Quality Review System

Map to:

- Input: files or directories
- Parser: language-specific scanning or AST if available
- Rules: security, style, complexity, secrets, dependency risks
- Findings: file, line, severity, rule id, message, suggestion
- Report: Markdown, JSON, console summary
- Config: enabled rules, severity threshold, ignored paths
- AI mock: provider interface returning explanatory suggestions

Minimum viable design:

- Built-in rules first
- Configurable rule registry
- Batch scan
- Deterministic report
- Optional mock AI analyzer behind an interface

### Customer Service / Chat Assistant

Map to:

- Input: user message
- Intent: classify problem
- Knowledge: FAQ, documents, order/status lookup
- Policy: when to answer, ask clarification, escalate
- Output: response plus confidence/source
- State: session context

Minimum viable design:

- Rule-based intent or simple retrieval
- Small knowledge base
- Escalation fallback
- Conversation transcript

### Order / Workflow System

Map to:

- Entity: order/task/ticket
- State machine: created, pending, approved, failed, completed
- Commands: create, update, cancel, query
- Rules: allowed transitions and validation
- Storage: in-memory or database depending on repo
- Output: state and audit trail

Minimum viable design:

- Explicit state transitions
- Idempotent operations if events are involved
- Clear error messages for invalid states

### Log / Data Analyzer

Map to:

- Input: log file, CSV, JSON lines, metrics
- Parser: line or record normalization
- Aggregator: counts, grouping, time windows
- Detector: thresholds, anomalies, patterns
- Output: summary report and details

Minimum viable design:

- Robust parsing
- Skip bad lines with warnings
- Deterministic summary
- Small sample fixture

### Permission / Review / Audit System

Map to:

- Subject: user/service/team
- Resource: file/API/data/object
- Action: read/write/approve/delete
- Policy: allow/deny/risk level
- Evidence: why decision was made
- Output: decision or audit report

Minimum viable design:

- Policy evaluator
- Explainable result
- Configurable rules
- Deny-by-default for missing policy

## Naming Heuristics

Use boring names:

- `Scanner`, `Analyzer`, `Rule`, `Finding`, `Report`, `Config`
- `Parser`, `Processor`, `Result`, `ValidationError`
- `Policy`, `Decision`, `Evidence`
- `State`, `Transition`, `Command`, `Handler`

Avoid clever names during interviews. Readability beats originality.
