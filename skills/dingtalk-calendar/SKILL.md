---
name: dingtalk-calendar
description: >
  View and manage DingTalk (钉钉) calendar — check today's agenda,
  upcoming meetings, create events, check availability, book meeting rooms.
  Use when the user asks about meetings, calendar, schedule, agenda, or events.
  Trigger phrases: "明天有什么会", "今天的日程", "这周有什么安排",
  "帮我建个会议", "日程", "日历", "有什么会议", "agenda", "schedule",
  "钉钉日程", "会议室", "查空闲".
---

# DingTalk Calendar — View & Manage Events

View and manage DingTalk calendar via `dws`.

**CLI**: `dws` (if not found, trigger `dingtalk-setup` skill)

## View Agenda

```
# List upcoming events
dws calendar event list --yes -f json

# Use --jq to extract key info
dws calendar event list --yes -f json --jq '.result[] | {id: .id, summary: .summary, start: .start.dateTime, end: .end.dateTime}'

# Check all flags
dws calendar event list --help
```

When the user asks for a specific date or range, use `--start` and `--end` flags if available:
```
dws calendar event list --start "2026-04-21T00:00:00+08:00" --end "2026-04-21T23:59:59+08:00" --yes -f json
```

**IMPORTANT**: All times use Beijing timezone (+08:00). When the user says "明天", calculate tomorrow's date. When they say "这周", calculate this week's Monday to Sunday.

## Create an Event

```
dws calendar event create --summary "会议标题" --start "2026-04-22T14:00:00+08:00" --end "2026-04-22T15:00:00+08:00" --yes

# Check all flags for inviting attendees, location, etc.
dws calendar event create --help
```

## Check Availability (Free/Busy)

```
dws calendar busy search --user-ids "<userId1,userId2>" --start "2026-04-22T00:00:00+08:00" --end "2026-04-22T23:59:59+08:00" --yes -f json
```

## Meeting Rooms

```
# List available meeting rooms
dws calendar room list --yes -f json

# Check room availability
dws calendar room --help
```

## Manage Participants

```
# Add participant to an event
dws calendar participant add --event-id <EVENT_ID> --help

# Remove participant
dws calendar participant remove --event-id <EVENT_ID> --help
```

## RSVP to an Event

```
dws calendar event rsvp --help
```

## Tips

- All times use Beijing timezone (+08:00)
- Always add `--yes` to skip interactive prompts
- Use `-f json` for structured output
- Use `--jq` to reduce output and save tokens
- Run `--help` before guessing flags
- `dws calendar` has 13 subcommands — check `dws calendar --help` for the full list

## Feedback: Report Issues

If a command fails and recovery doesn't work, help the user submit a GitHub Issue.

### 提交 issue 流程（优先自动提交）

**Step 1: 检查 gh CLI 登录态**

```bash
gh auth status
```

**Step 2a: 如果已登录 GitHub → 直接帮用户提 issue**

整理好以下信息，展示给用户确认：
- 标题：`[dingtalk-calendar] <一句话描述问题>`
- 内容：错误日志、`node --version`、`dws --version`、操作系统、复现步骤

用户确认后，执行：

```bash
gh issue create --repo heran11011/cola-dingtalk-skills \
  --title "[dingtalk-calendar] 问题标题" \
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
