---
name: dingtalk-messages
description: >
  Send and manage DingTalk (钉钉) group messages via bot. Use when the user
  asks to send messages, check groups, or communicate through DingTalk.
  Trigger phrases: "发消息到钉钉群", "钉钉群消息", "帮我发个消息",
  "通知一下群里", "群里说一下", "send dingtalk message", "group message",
  "钉钉通知", "发到工作群".
  NOTE: DingTalk messaging is primarily send-oriented (bot sends to groups).
  Reading historical group messages is not supported via dws CLI.
---

# DingTalk Messages — Send & Manage

Send messages to DingTalk groups and individuals via `dws` bot commands.

**CLI**: `dws` (if not found, trigger `dingtalk-setup` skill)

## Important Limitation

Unlike Feishu/Lark, DingTalk's CLI is **send-oriented** — you can send messages to groups via bot, but **cannot read historical group messages**. If the user asks to "read messages" or "summarize chat", explain this limitation and suggest they check DingTalk directly.

## How It Works

### Step 1: Find the group

```
dws chat group search --keyword "群名关键词" --yes -f json
```

Returns group info including `openConversationId` — save it for sending.

If unsure which group, ask the user.

### Step 2: Send messages

**Via Bot (requires robot-code):**
```
dws chat message send-by-bot --robot-code <BOT_CODE> --group <GROUP_ID> --title "标题" --text "消息内容" --yes
```

**Via Webhook (simpler, no robot-code needed):**
```
dws chat bot webhook send --webhook-url <WEBHOOK_URL> --text "消息内容" --yes
```

**Send Markdown:**
```
dws chat bot webhook send --webhook-url <WEBHOOK_URL> --markdown "## 标题\n内容" --yes
```

To get the webhook URL, the user needs to add a "Custom Robot" to their DingTalk group and copy the webhook URL.

### Step 3: Other message operations

```
# Recall a message
dws chat message recall --message-id <MSG_ID> --yes

# Send DING (urgent notification that must be acknowledged)
dws ding message send --user-ids "<userId1,userId2>" --text "紧急通知内容" --yes
```

## Responding to messages

**SAFETY: NEVER send a message without explicit user confirmation.** Always draft and confirm first.

When the user asks to send a message:
1. Draft the message content
2. Show the draft to the user
3. Wait for confirmation
4. Then send

## Tips

- Always add `--yes` to skip interactive prompts
- Use `-f json` when you need to parse the response
- Use `--jq` to extract specific fields and save tokens
- For urgent notifications, use `dws ding message send` instead of regular messages
- Run `dws chat --help` for all available subcommands

## Feedback: Report Issues

If a command fails and recovery doesn't work, help the user submit a GitHub Issue. Collect the error output, OS, and dws version, then draft the Issue:

```
Title: [dingtalk-messages] <one-line error summary>
Body: Environment info + error output + steps to reproduce
```

> 这个问题我暂时无法自动修复，你可以在这里反馈：
> https://github.com/heran11011/cola-dingtalk-skills/issues/new
