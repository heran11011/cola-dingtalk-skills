---
name: dingtalk-aitables
description: >
  Query and manage DingTalk (钉钉) AITable (AI 表格/多维表格) data — list bases,
  read records, write records, query with filters. Use when the user asks about
  多维表格, AI表格, aitable, spreadsheet data, table records, or any data stored
  in DingTalk tables. Trigger phrases: "查一下表格", "AI表格", "多维表格",
  "表格里的数据", "帮我加一条记录", "aitable", "查数据", "query data",
  "spreadsheet", "database records".
---

# DingTalk AITable — Query & Manage

Query and manage DingTalk AITable (多维表格) data via `dws`.

**CLI**: `dws` (if not found, trigger `dingtalk-setup` skill)

## Prerequisites

AITable operations need a `base-id` and usually a `table-id`. The user should provide these, or you can list all bases first.

## List Bases

```
dws aitable base list --yes -f json
```

## List Tables in a Base

```
dws aitable table list --base-id <BASE_ID> --yes -f json
```

## List Fields (understand table structure)

Always list fields first if you don't know the table structure:

```
dws aitable field list --base-id <BASE_ID> --table-id <TABLE_ID> --yes -f json
```

## Query Records

```
# List all records
dws aitable record query --base-id <BASE_ID> --table-id <TABLE_ID> --yes -f json

# Limit results
dws aitable record query --base-id <BASE_ID> --table-id <TABLE_ID> --limit 10 --yes -f json

# Use --jq for specific fields
dws aitable record query --base-id <BASE_ID> --table-id <TABLE_ID> --yes -f json --jq '.result[]'

# Check all flags for filtering, sorting
dws aitable record query --help
```

## Create a Record

```
dws aitable record create --base-id <BASE_ID> --table-id <TABLE_ID> --data '{"fields":{"Name":"value","Status":"active"}}' --yes
```

## Update a Record

```
dws aitable record update --base-id <BASE_ID> --table-id <TABLE_ID> --record-id <RECORD_ID> --data '{"fields":{"Status":"done"}}' --yes
```

## Delete a Record

```
dws aitable record delete --base-id <BASE_ID> --table-id <TABLE_ID> --record-id <RECORD_ID> --yes
```

## Tips

- Always list fields first if you don't know the table structure
- Always add `--yes` to skip interactive prompts
- Use `-f json` for structured output
- Use `--jq` to extract specific fields and reduce token usage
- Run `--help` on any subcommand before guessing flags
- When presenting data, format it as a clear table
- `dws aitable` has 20 subcommands — check `dws aitable --help` for the full list

## Advanced: Schema Discovery

Use `dws schema` to discover AITable capabilities dynamically:
```
dws schema aitable.query_records --jq '.tool.parameters'
```

## Feedback: Report Issues

If a command fails and recovery doesn't work, help the user submit a GitHub Issue.

### 提交 issue 流程（优先自动提交）

**Step 1: 检查 gh CLI 登录态**

```bash
gh auth status
```

**Step 2a: 如果已登录 GitHub → 直接帮用户提 issue**

整理好以下信息，展示给用户确认：
- 标题：`[dingtalk-aitables] <一句话描述问题>`
- 内容：错误日志、`node --version`、`dws --version`、操作系统、复现步骤

用户确认后，执行：

```bash
gh issue create --repo heran11011/cola-dingtalk-skills \
  --title "[dingtalk-aitables] 问题标题" \
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
