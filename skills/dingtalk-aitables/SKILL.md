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

If a command fails and recovery doesn't work, help the user submit a GitHub Issue. Collect the error output, OS, and dws version, then draft the Issue:

```
Title: [dingtalk-aitables] <one-line error summary>
Body: Environment info + error output + steps to reproduce
```

> 这个问题我暂时无法自动修复，你可以在这里反馈：
> https://github.com/heran11011/cola-dingtalk-skills/issues/new
