# Loop Patterns

Use these patterns to choose the simplest loop that can satisfy the user's goal.

## Single-Agent Local Loop

Use for code changes, document production, local file processing, reports, and data cleanup.

```text
Read inputs -> Plan edits -> Modify files -> Run checks -> Inspect diff/output -> Fix or stop
```

Good verification:

- Tests pass
- Output file exists
- Diff matches intent
- No unrelated files changed

## Browser-Agent Loop

Use for web pages, dashboards, platform QA, account workflows, and form completion.

```text
Open page -> Confirm URL/state -> Read visible content -> Decide next action -> Click/type -> Verify page state -> Pause at approval gate
```

Add approval before submit, publish, profile save, purchase, payment, or message send.

Good verification:

- URL matches expected domain
- Visible confirmation text exists
- Screenshot or page text confirms state
- No hidden assumption about login or identity

## Research Loop

Use for market scans, technical source gathering, evidence briefs, and current events.

```text
Define question -> Search primary sources -> Collect evidence -> Cross-check claims -> Synthesize -> Cite sources
```

Good verification:

- Current or date-stable sources are separated
- Direct evidence is separated from inference
- Weak evidence is labeled
- URLs are included

## QA and Bug Loop

Use for software testing, uTest-style bug work, browser checks, and regression review.

```text
Set environment -> Reproduce -> Capture evidence -> Classify severity -> Report -> Respond to info requests -> Verify status
```

Good verification:

- Steps to reproduce are clear
- Actual and expected behavior are separated
- Evidence is attached or cited
- Follow-up requests are answered before closing

## MCP or Tool Loop

Use when an agent needs repeatable access to external systems.

```text
Identify data/tool need -> Choose connector -> Define allowed actions -> Call tool -> Validate result -> Record state
```

Good verification:

- Tool permissions are explicit
- Returned data shape is checked
- Tool failures have fallback behavior
- Sensitive data is not exposed unnecessarily

## Multi-Agent Loop

Use only when tasks are independent or require different specialties.

```text
Supervisor plans -> Assign subtasks -> Agents execute -> Supervisor verifies -> Merge outputs -> Human review
```

Avoid multi-agent workflows when a single loop is enough. Multi-agent systems add coordination cost and more failure modes.

## Scheduling Loop

Use for recurring monitors and reminders.

```text
Trigger -> Fetch state -> Compare to last state -> Decide action -> Notify or update -> Store checkpoint
```

Good verification:

- Checkpoint exists
- Duplicate notifications are avoided
- Timezone and frequency are explicit
- Failures are visible to the user
