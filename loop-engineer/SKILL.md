---
name: loop-engineer
description: Design reliable AI agent loops and agentic workflows. Use when the user wants to automate a task with AI agents, Claude Code, Codex, browser agents, MCP tools, n8n-style workflows, repeated research, QA/testing loops, content pipelines, or any process that needs planning, tool use, verification, retries, human approval gates, and operational safeguards.
---

# Loop Engineer

Use this skill to turn a vague automation idea into a controlled AI execution loop. Focus on the loop architecture, success criteria, verification, failure recovery, and human control points before implementation.

## Core Rule

Never treat "the AI can answer" as equivalent to "the AI can reliably execute." A loop is only ready when it has:

- A concrete objective and observable success criteria
- Known inputs, tools, permissions, and environment boundaries
- A step-by-step observe-plan-act-check-reflect cycle
- Verification for important outputs
- Human approval gates for risky actions
- Stop conditions and recovery paths

## Workflow

### 1. Define the Objective

Convert the user's request into a concrete task contract:

- Goal: what outcome should exist after the loop runs
- Inputs: files, URLs, accounts, APIs, prompts, datasets, messages, or manual user data
- Output: report, file, code change, submitted form, browser state, dataset, dashboard, or notification
- Success criteria: how to prove the output is correct
- Frequency: one-off, scheduled, continuous monitor, or event-triggered
- Risk level: low, medium, or high

If the request is vague but safe, state reasonable assumptions and continue. Ask only when missing information would make the loop unsafe or impossible.

### 2. Map the Environment

List what the loop can observe and control:

- Surfaces: browser, local files, terminal, APIs, email, sheets, databases, GitHub, third-party platforms
- Tools: exact tools or connectors available
- Permissions: read-only, write, submit, publish, payment, delete, account settings
- Constraints: login barriers, rate limits, captchas, platform policy, cost limits, private data

Do not design automation that bypasses platform controls, captchas, paywalls, account restrictions, or safety checks.

### 3. Decompose the Loop

Use this canonical structure:

```text
Observe -> Plan -> Act -> Check -> Reflect -> Retry or Escalate
```

For each stage, define:

- Input
- Action
- Output
- Failure signal
- Maximum retries or stop condition

Prefer a minimal runnable loop first. Add parallelism, memory, scheduling, or multi-agent delegation only after the single-loop version is clear.

### 4. Add Control Gates

Require explicit user confirmation before actions that:

- Submit forms, applications, reviews, or bug reports
- Publish public content or send messages
- Change account/profile/payment/security settings
- Spend money, trigger purchases, request refunds, or handle banking data
- Delete, overwrite, or mass-edit data
- Contact people or act as the user on a platform
- Upload private documents, identity data, credentials, or sensitive files

State what can be automated without confirmation and what must pause.

For detailed categories, read `references/risk-gates.md`.

### 5. Build Verification

Every loop must define at least one verification method:

- Programmatic: tests, exit codes, schema validation, row counts, API status, diff checks
- Visual: screenshot comparison, page state, visible confirmation text
- Data quality: source count, deduplication, timestamp checks, field completeness
- Human review: checklist, approval prompt, sample inspection

If verification is weak, say so and constrain the loop's autonomy.

### 6. Plan Recovery

Define what happens when the loop fails:

- Retry with the same method
- Try a safer fallback
- Reduce scope
- Ask the user for input
- Stop and report the failure

Never allow unbounded retries. Default maximum retries: 2 for web actions, 3 for local deterministic operations.

### 7. Deliver the Loop Spec

Unless the user asks for implementation immediately, deliver a clear loop specification using this format:

```markdown
## Loop Brief
Goal:
Inputs:
Output:
Success criteria:
Run mode:
Risk level:
Human approval gates:

## Loop Design
Observe:
Plan:
Act:
Check:
Reflect:
Retry/Escalate:

## Tools Needed
- Tool:

## Verification Plan
- Automatic checks:
- Human checks:
- Failure signals:

## First Runnable Version
1.
2.
3.

## Iteration Plan
V1:
V2:
V3:
```

For more templates, read `references/output-templates.md`.

## Design Patterns

Use these default patterns:

- Single-agent local loop: best for file/code/report tasks
- Browser-agent loop: best for web tasks, with more approval gates
- Research loop: search, collect, verify, synthesize, cite
- QA loop: reproduce, observe, report, verify fix
- Multi-agent loop: use only when subtasks are independent and verification is clear
- MCP/tool loop: use when the agent needs stable access to external data or tools

For pattern details, read `references/loop-patterns.md`.

## Quality Bar

A good Loop Engineer answer is concrete enough that another agent or human can execute the first version. It should include boundaries, not just ambition. It should make the smallest useful loop work before expanding scope.
