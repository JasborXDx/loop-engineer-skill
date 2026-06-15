# Loop Engineer Skill

`loop-engineer` is a Codex skill for designing reliable AI agent loops and agentic workflows.

It helps turn vague automation ideas into executable, verifiable workflows with clear success criteria, tool boundaries, retry logic, and human approval gates.

## What This Skill Does

Use this skill when you want an AI agent to design a repeatable workflow such as:

- Daily project or opportunity screening
- Browser-based task workflows
- AI research and source collection loops
- QA, bug reproduction, and test reporting loops
- Claude Code / Codex coding workflows
- MCP, API, or tool-connected agent workflows
- n8n-style automation planning
- Human-in-the-loop approval systems

The core loop pattern is:

```text
Observe -> Plan -> Act -> Check -> Reflect -> Retry or Escalate
```

The skill forces the agent to define:

- The actual goal
- Inputs and outputs
- Success criteria
- Tools and environment boundaries
- Verification checks
- Failure and retry behavior
- Human approval gates for risky actions

## What This Skill Is Not

This is not a prompt collection and not a promise of full automation.

It is designed to make AI workflows safer and more reliable. It should not be used to bypass platform controls, captchas, account restrictions, payment safeguards, or human approval requirements.

## Repository Structure

```text
loop-engineer/
  SKILL.md
  agents/
    openai.yaml
  references/
    loop-patterns.md
    output-templates.md
    risk-gates.md
```

### `SKILL.md`

The main skill instructions. Codex reads this when the skill is triggered.

### `agents/openai.yaml`

UI metadata for the skill, including display name, short description, and default prompt.

### `references/loop-patterns.md`

Reusable loop patterns for browser agents, research loops, QA loops, MCP/tool loops, scheduling loops, and multi-agent loops.

### `references/risk-gates.md`

Rules for deciding when an AI agent can act automatically and when it must stop for human confirmation.

### `references/output-templates.md`

Reusable output templates for loop specs, readiness checks, failure reports, and approval prompts.

## Installation

Clone this repository:

```bash
git clone https://github.com/JasborXDx/loop-engineer-skill.git
```

Copy the `loop-engineer` folder into your Codex skills directory.

On Windows:

```powershell
Copy-Item -Recurse .\loop-engineer C:\Users\<YOUR_USER>\.codex\skills\loop-engineer
```

On macOS or Linux:

```bash
cp -R ./loop-engineer ~/.codex/skills/loop-engineer
```

Restart or refresh Codex if the skill does not appear immediately.

## How To Use

Invoke it explicitly:

```text
Use $loop-engineer to turn this task into a reliable AI agent loop:
I want to check uTest every morning, find projects that match my profile, and remind me which ones I can apply to.
```

Chinese prompt example:

```text
用 loop-engineer 帮我设计一个自动化闭环：
我想每天自动搜集 uTest 上适合我的项目，筛选出来，然后提醒我哪些可以申请。
```

Better input format:

```text
Use $loop-engineer:
Goal: Check uTest every day for suitable projects.
Inputs: uTest dashboard, projects board, my devices, languages, and location.
Output: A ranked list of projects I can apply to.
Limits: Do not apply or submit forms without my confirmation.
```

## Expected Output

The skill should produce a structured loop design like this:

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

## Example Use Case

User request:

```text
Use $loop-engineer to design a workflow that checks GitHub Trending every morning, finds repos with business potential, and creates a short report.
```

Expected behavior:

- Define the daily input source
- Decide what counts as business potential
- Separate trend heat from real demand
- Add verification steps and source links
- Store previous results to avoid duplicate alerts
- Output a ranked report
- Avoid posting, messaging, or opening issues without approval

## Safety Rules

The skill requires human confirmation before actions such as:

- Submitting forms or applications
- Publishing posts or comments
- Sending emails or messages
- Changing account/profile/payment/security settings
- Spending money or using payment data
- Uploading private documents or sensitive files
- Accepting legal agreements or project commitments
- Deleting or mass-editing data

The skill should stop instead of automating when a task requires:

- Bypassing captchas or anti-bot systems
- Misrepresenting identity, location, skills, or device access
- Submitting fake results, fake bug reports, or fake reviews
- Exposing credentials or secrets

## Development Notes

This skill intentionally keeps the main `SKILL.md` concise and places reusable details in `references/`. That keeps the context lightweight while still making deeper guidance available when needed.

The first version does not include scripts because the useful work is mostly workflow design and risk control. Scripts can be added later for repeated concrete workflows.
