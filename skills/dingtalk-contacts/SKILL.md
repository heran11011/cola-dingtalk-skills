---
name: dingtalk-contacts
description: >
  Search and query DingTalk (钉钉) contacts — find users by name or phone,
  view departments, get user details. Use when the user asks about colleagues,
  contacts, phone numbers, departments, or organizational structure.
  Trigger phrases: "帮我找一下张三", "通讯录", "联系方式", "部门成员",
  "谁的手机号是", "find contact", "search user", "department members",
  "钉钉通讯录", "组织架构".
---

# DingTalk Contacts — Search & Query

Search and query DingTalk organization contacts via `dws`.

**CLI**: `dws` (if not found, trigger `dingtalk-setup` skill)

## Search Users by Name

```
dws contact user search --keyword "姓名或关键词" --yes -f json
```

Use `--jq` to extract useful fields:
```
dws contact user search --keyword "张三" --yes -f json --jq '.result[] | {name: .name, userId: .userId, dept: .deptName}'
```

## Find User by Phone Number

```
dws contact user get-by-mobile --mobile "13800138000" --yes -f json
```

## Get Current User Info

```
dws contact user get-self --yes -f json
```

Useful for getting your own userId, department, etc.

## Department Operations

```
# List all departments
dws contact dept list --yes -f json

# List members of a department
dws contact dept user-list --dept-id <DEPT_ID> --yes -f json

# Check all flags
dws contact dept --help
```

## Tips

- Always add `--yes` to skip interactive prompts
- Use `-f json` for structured output
- Use `--jq` to extract specific fields (name, phone, department)
- Phone numbers may be partially hidden due to privacy settings
- Run `--help` on any subcommand before guessing flags
- `dws contact` has 6 subcommands — check `dws contact --help` for the full list

## Privacy Note

Contact information is subject to the organization's privacy policies. Some fields (phone, email) may be hidden or require additional permissions.

## Feedback: Report Issues

If a command fails and recovery doesn't work, help the user submit a GitHub Issue.

### 提交 issue 流程（优先自动提交）

**Step 1: 检查 gh CLI 登录态**

```bash
gh auth status
```

**Step 2a: 如果已登录 GitHub → 直接帮用户提 issue**

整理好以下信息，展示给用户确认：
- 标题：`[dingtalk-contacts] <一句话描述问题>`
- 内容：错误日志、`node --version`、`dws --version`、操作系统、复现步骤

用户确认后，执行：

```bash
gh issue create --repo heran11011/cola-dingtalk-skills \
  --title "[dingtalk-contacts] 问题标题" \
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


---

## ⚠️ Security / 安全提示

When constructing shell commands, always sanitize user input to prevent command injection. Wrap dynamic values in single quotes and escape any embedded single quotes. Never pass raw user input directly into shell command strings.

构造 shell 命令时，务必对用户输入进行转义以防止命令注入。用单引号包裹动态值，并转义其中的单引号。不要将原始用户输入直接拼接到命令字符串中。
