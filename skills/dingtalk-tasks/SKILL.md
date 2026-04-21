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

If a command fails and recovery doesn't work, help the user submit a GitHub Issue. Collect the error output, OS, and dws version, then draft the Issue:

```
Title: [dingtalk-tasks] <one-line error summary>
Body: Environment info + error output + steps to reproduce
```

> 这个问题我暂时无法自动修复，你可以在这里反馈：
> https://github.com/heran11011/cola-dingtalk-skills/issues/new
