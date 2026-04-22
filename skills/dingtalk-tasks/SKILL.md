---
name: dingtalk-tasks
description: >
  View and manage DingTalk (钉钉) todo tasks — list my tasks, create tasks,
  complete tasks. Use when the user asks about their tasks, to-do items,
  pending work, or wants to create/complete a task. Trigger phrases:
  "我有什么待办", "钉钉待办", "帮我创建一个任务", "任务完成了",
  "还有什么没做", "to-do", "todo list", "my tasks", "pending tasks",
  "create a task", "complete task", "钉钉任务".
---

# DingTalk Tasks — View & Manage Todo

Manage DingTalk todo tasks via `dws`.

**CLI**: `dws` (if not found, trigger `dingtalk-setup` skill)

## View My Tasks

```
dws todo task list --yes -f json
```

Present tasks sorted by due date. Highlight overdue items.

Use `--jq` to extract key fields:
```
dws todo task list --yes -f json --jq '.result[] | {id: .taskId, title: .subject, due: .dueTime, done: .done}'
```

## Create a Task

```
# Basic task
dws todo task create --title "任务标题" --yes

# With executor (assign to someone, use userId)
dws todo task create --title "任务标题" --executors "<userId>" --yes

# With due date (ISO 8601, Beijing timezone)
dws todo task create --title "任务标题" --executors "<userId>" --due "2026-04-25T18:00:00+08:00" --yes

# Check all flags
dws todo task create --help
```

To find your own userId:
```
dws contact user get-self --yes -f json --jq '.result[0].userId'
```

## Complete a Task

```
dws todo task done --task-id <task_id> --yes
```

## Get Task Details

```
dws todo task get --task-id <task_id> --yes -f json
```

## Update a Task

```
dws todo task update --task-id <task_id> --title "新标题" --yes
```

## Delete a Task

```
dws todo task delete --task-id <task_id> --yes
```

## Tips

- Always add `--yes` to skip interactive prompts
- Always run `--help` on subcommands to confirm exact flags
- When creating tasks from conversations, extract the action item clearly
- Use `-f json` for structured output, `--jq` for field extraction

## Feedback: Report Issues

If a command fails and recovery doesn't work, help the user submit a GitHub Issue.

### 提交 issue 流程（优先自动提交）

**Step 1: 检查 gh CLI 登录态**

```bash
gh auth status
```

**Step 2a: 如果已登录 GitHub → 直接帮用户提 issue**

整理好以下信息，展示给用户确认：
- 标题：`[dingtalk-tasks] <一句话描述问题>`
- 内容：错误日志、`node --version`、`dws --version`、操作系统、复现步骤

用户确认后，执行：

```bash
gh issue create --repo heran11011/cola-dingtalk-skills \
  --title "[dingtalk-tasks] 问题标题" \
  --body "整理好的问题描述"
```

告诉用户：
> ✅ 已帮你提交 issue，开发者会收到通知并尽快处理。

**Step 2b: 如果未登录 GitHub → 给链接**

告诉用户：
> 你的电脑还没有登录 GitHub CLI，我没办法直接帮你提交。
> 你可以手动在这里提 issue：
> https://github.com/heran11011/cola-dingtalk-skills/issues/new
>
> 或者先登录 GitHub CLI（`gh auth login`），下次我就能直接帮你提交了。

提交 issue 时，引导用户附上：
- 错误日志（终端输出）
- Node.js 版本（`node --version`）
- dws 版本（`dws --version`）
- 操作系统
