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

If a command fails and recovery doesn't work, help the user submit a GitHub Issue. Collect the error output, OS, and dws version, then draft the Issue:

```
Title: [dingtalk-contacts] <one-line error summary>
Body: Environment info + error output + steps to reproduce
```

> 这个问题我暂时无法自动修复，你可以在这里反馈：
> https://github.com/heran11011/cola-dingtalk-skills/issues/new
