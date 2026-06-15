# Loop Engineer Skill

中文 | [English](#english-version)

`loop-engineer` 是一个 Codex skill，用来设计可靠的 AI agent 闭环和 agentic workflow。

它的目标不是写一段 prompt，而是把一个模糊的自动化想法，整理成可以执行、可以验证、可以失败恢复、并且带有人类确认节点的 AI 工作流。

## 这个 Skill 能做什么

当你想让 AI agent 设计一个可重复执行的流程时，可以使用这个 skill，例如：

- 每天筛选项目、机会或任务
- 浏览器自动化任务流程
- AI 资料搜集和来源验证流程
- QA、bug 复现、测试报告流程
- Claude Code / Codex 编程工作流
- MCP、API、数据库或工具连接型 agent workflow
- n8n 风格的自动化流程规划
- 带人工确认节点的人机协作系统

核心闭环模式是：

```text
Observe -> Plan -> Act -> Check -> Reflect -> Retry or Escalate
```

这个 skill 会强制 agent 先定义清楚：

- 真实目标是什么
- 输入和输出是什么
- 成功标准是什么
- 可以使用哪些工具和环境
- 怎么验证结果
- 失败后怎么重试或降级
- 哪些高风险动作必须人工确认

## 这个 Skill 不是什么

它不是 prompt 合集，也不是“全自动完成一切”的承诺。

它的用途是让 AI workflow 更可靠、更安全。它不应该被用于绕过平台限制、验证码、账号访问控制、付款保护、人工确认要求或其他安全机制。

## 仓库结构

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

主 skill 文件。Codex 触发这个 skill 时会读取这里的核心流程。

### `agents/openai.yaml`

Skill 的 UI 元数据，包括显示名称、简短介绍和默认调用 prompt。

### `references/loop-patterns.md`

常见闭环模式参考，包括 browser agent、research loop、QA loop、MCP/tool loop、scheduling loop 和 multi-agent loop。

### `references/risk-gates.md`

风险控制规则，用来判断哪些动作可以自动执行，哪些动作必须停下来让人确认。

### `references/output-templates.md`

输出模板，包括 loop spec、自动化准备检查、失败报告和人工确认提示。

## 安装方法

克隆这个仓库：

```bash
git clone https://github.com/JasborXDx/loop-engineer-skill.git
```

把 `loop-engineer` 文件夹复制到你的 Codex skills 目录。

Windows:

```powershell
Copy-Item -Recurse .\loop-engineer C:\Users\<YOUR_USER>\.codex\skills\loop-engineer
```

macOS 或 Linux:

```bash
cp -R ./loop-engineer ~/.codex/skills/loop-engineer
```

如果 Codex 没有立刻识别这个 skill，重启或刷新 Codex。

## 使用方法

显式调用：

```text
Use $loop-engineer to turn this task into a reliable AI agent loop:
I want to check uTest every morning, find projects that match my profile, and remind me which ones I can apply to.
```

中文调用示例：

```text
用 loop-engineer 帮我设计一个自动化闭环：
我想每天自动搜集 uTest 上适合我的项目，筛选出来，然后提醒我哪些可以申请。
```

更清晰的输入格式：

```text
Use $loop-engineer:
目标：每天检查 uTest 上适合我的项目。
输入：uTest dashboard、projects board、我的设备、语言和地区。
输出：一份按优先级排序的可申请项目清单。
限制：不要自动申请，也不要自动提交表单，必须先问我确认。
```

## 预期输出格式

这个 skill 通常会输出类似下面的结构：

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

## 示例场景

用户请求：

```text
Use $loop-engineer to design a workflow that checks GitHub Trending every morning, finds repos with business potential, and creates a short report.
```

预期行为：

- 定义每天要检查的数据来源
- 判断什么叫“有商业潜力”
- 区分热度和真实需求
- 增加来源链接和验证步骤
- 保存上一次结果，避免重复提醒
- 输出排序后的简短报告
- 不在没有确认的情况下发帖、发消息或创建 issue

## 安全规则

以下动作必须先获得人工确认：

- 提交表单或申请
- 发布帖子、评论或评价
- 发送邮件或私信
- 修改账号资料、付款信息、隐私设置或安全设置
- 花钱、付款、退款或使用支付数据
- 上传私人文件、身份证明、合同、凭据或敏感资料
- 接受法律协议、NDA 或项目承诺
- 删除、覆盖或批量修改数据

以下情况应该停止，而不是继续自动化：

- 绕过验证码、反爬系统或平台访问控制
- 虚假声明身份、地区、技能、设备或账号权限
- 提交虚假测试结果、虚假 bug report 或虚假评论
- 暴露账号密码、token、密钥或其他敏感凭据

## 开发说明

这个 skill 有意保持 `SKILL.md` 精简，把可复用细节放在 `references/` 目录里。这样每次触发时上下文更轻，但需要深入细节时仍然可以读取参考文件。

第一版没有包含脚本，因为它最核心的价值是 workflow 设计、验证设计和风险控制。以后如果某类任务变得高频，可以继续添加 `scripts/`。

---

## English Version

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
