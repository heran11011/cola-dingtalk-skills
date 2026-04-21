---
name: dingtalk-setup
description: >
  Set up DingTalk (钉钉) integration for Cola — install dws CLI, authenticate,
  and verify connection. Use when the user wants to connect DingTalk, or when
  any dingtalk-* skill fails because dws is not installed or not authenticated.
  Trigger phrases: "连接钉钉", "接入钉钉", "配置钉钉", "钉钉设置",
  "dingtalk setup", "connect dingtalk", "dws not found", "钉钉授权".
  Also trigger when you detect dws errors like "command not found",
  "not authenticated", or "token expired".
  PROACTIVE: If dws is not installed or not authenticated, start this
  setup flow immediately without waiting for user to ask.
---

# DingTalk Setup — Connect Cola to DingTalk

**Design goal**: FULLY AUTOMATIC. Cola detects what's missing and installs everything. The user only clicks in the browser for DingTalk authorization.

## Cross-Platform Notes

- Run commands **one at a time**
- `dws` commands are cross-platform (Go binary), no shell differences
- Always add `--yes` to skip interactive prompts

## Behavior: Be Proactive

When this skill is loaded, **immediately** run Step 0. If DingTalk is not configured, tell the user:

> 我检测到你安装了钉钉集成技能包，可以帮你发群消息、管待办、查日程、搜通讯录、查表格。
> 现在帮你连接钉钉，只需要在浏览器里登录授权就好。

Then proceed directly without stopping.

## Step 0: Diagnose Current State

```
node --version
```
If fails → Step 0.5

```
dws --version
```
If fails → Step 1

```
dws auth status --yes -f json
```
- Not authenticated → Step 2
- Token expired → Step 2
- Authenticated → "You're Ready"

## Step 0.5: Auto-Install Node.js

**Windows:**
```
winget install OpenJS.NodeJS.LTS --accept-package-agreements --accept-source-agreements
```

**macOS:**
```
brew install node
```
If `brew` is not available, tell the user: "请前往 https://nodejs.org 下载最新 LTS 版本安装"

Then proceed to Step 1.

## Step 1: Install dws

**macOS / Linux:**
```
curl -fsSL https://raw.githubusercontent.com/DingTalk-Real-AI/dingtalk-workspace-cli/main/scripts/install.sh | sh
```

**Windows (PowerShell):**
```
irm https://raw.githubusercontent.com/DingTalk-Real-AI/dingtalk-workspace-cli/main/scripts/install.ps1 | iex
```

**Fallback (npm):**
```
npm install -g dingtalk-workspace-cli
```

Verify:
```
dws --version
```

**macOS note**: If "cannot be opened" error, run:
```
xattr -d com.apple.quarantine $(which dws)
```

Then proceed to Step 2.

## Step 2: Authenticate

```
dws auth login
```

This opens the browser automatically. The user selects their organization and authorizes.

For headless environments (Docker, SSH, CI):
```
dws auth login --device
```

Tell the user:
> 浏览器会自动打开钉钉登录页面，选择你的组织并授权即可。
> 如果你的组织还没开通 CLI 访问，页面会提示你向管理员申请，管理员一键审批后重新运行即可。

After authorization, verify:
```
dws auth status --yes -f json
```

## Step 3: Verify and Smoke Test

```
dws contact user get-self --yes -f json
```

This should return the current user's info. If it works, everything is connected.

## You're Ready

> 钉钉已连接成功！你现在可以直接跟我说：
> - "帮我发个消息到工作群" — 发送钉钉群消息
> - "我有什么待办" — 查看钉钉待办
> - "明天有什么会" — 查看日程
> - "帮我找一下张三的联系方式" — 搜索通讯录
> - "查一下表格里的数据" — 查询 AI 表格
>
> 试试看？

## Error Recovery

| 错误 | 解决 |
|------|------|
| `node` not found | Auto-install: brew (Mac) / winget (Win) |
| `dws` not found | curl install script or `npm install -g dingtalk-workspace-cli` |
| `not authenticated` | `dws auth login` |
| `token expired` | `dws auth login` (re-authenticate) |
| Organization not enabled | User needs to request admin approval, then re-run `dws auth login` |
| macOS quarantine | `xattr -d com.apple.quarantine $(which dws)` |
| Network timeout | Check network, try again |

## Feedback: Report Unresolved Issues

If the above recovery steps don't work, help the user submit a GitHub Issue:

1. Collect: error message, OS, `node --version`, `dws --version`, `dws auth status` output
2. Draft the Issue body:

```
Title: [dingtalk-setup] <one-line error summary>

**Environment**
- OS: <Windows/macOS/Linux + version>
- Node: <version>
- dws: <version>
- Cola: <version>

**What happened**
<paste error output>

**Steps to reproduce**
1. ...
```

3. Tell the user:
> 这个问题我暂时无法自动修复。你可以在这里反馈：
> https://github.com/heran11011/cola-dingtalk-skills/issues/new
