# Output Templates

Use these templates when the user needs a clear loop design or implementation plan.

## Compact Loop Spec

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

## Automation Readiness Checklist

```markdown
## Readiness
- Objective is concrete:
- Inputs are available:
- Tools are available:
- Permissions are understood:
- Success criteria are measurable:
- Verification exists:
- Risk gates are defined:
- Stop conditions exist:
- First runnable version is small:
```

## Failure Report

```markdown
## Loop Failure
Stage:
Expected:
Actual:
Evidence:
Likely cause:
Retried:
Next safest action:
Needs user input:
```

## Human Approval Prompt

```markdown
I am at a control gate.

Action:
External effect:
Data involved:
Risk:
Verification so far:

Confirm whether I should continue.
```
