> ⚠️ **Disclaimer / 免责声明**
> 
> This is a community project, NOT officially maintained by DingTalk or Alibaba.
> Use at your own risk. The author is not responsible for any data loss or security issues.
> 
> 本项目为社区作品，**非钉钉（DingTalk）/ 阿里巴巴官方提供或维护**。使用风险自负，作者不对任何数据丢失或安全问题承担责任。

# Cola DingTalk Skills - 钉钉集成技能包

> v1.0.0

[English](#english) | [中文](#中文)

---

## 中文

### 简介

为 [Cola](https://cola.dev) 打造的钉钉（DingTalk）集成技能包。安装后，你可以用自然语言让 Cola 帮你操作钉钉——发消息、查日程、管待办、查通讯录、操作 AI 表格，一句话搞定。

基于钉钉官方 CLI 工具 [dws](https://github.com/nicepkg/dws)（dingtalk-workspace-cli），专为 AI Agent 设计。

### 包含的 Skills

| Skill | 功能 | 触发示例 |
|-------|------|---------|
| **dingtalk-setup** | 钉钉连接引导 | "帮我连接钉钉" |
| **dingtalk-messages** | 群消息发送 | "发消息到钉钉群" |
| **dingtalk-tasks** | 待办管理 | "我有什么待办" |
| **dingtalk-calendar** | 日历/日程管理 | "明天有什么会" |
| **dingtalk-contacts** | 通讯录查询 | "帮我找一下张三" |
| **dingtalk-aitables** | AI 表格操作 | "查一下表格里的数据" |

### 安装

#### 方法一：一键安装（推荐）

**macOS / Linux：**
```bash
git clone https://github.com/heran11011/cola-dingtalk-skills.git
cd cola-dingtalk-skills
chmod +x install.sh
./install.sh
```

**Windows：**
```cmd
git clone https://github.com/heran11011/cola-dingtalk-skills.git
cd cola-dingtalk-skills
install.bat
```

#### 方法二：手动安装

把 `skills/` 目录下的 6 个文件夹复制到 Cola 的 skills 目录：

| 系统 | 路径 |
|------|------|
| macOS / Linux | `~/.cola/mods/default/skills/` |
| Windows | `%USERPROFILE%\.cola\mods\default\skills\` |

### 前置条件

- [Cola](https://cola.dev)
- [Node.js](https://nodejs.org)（dws 的 npm 安装方式需要）

不需要提前安装 dws——对 Cola 说"帮我连接钉钉"，它会自动引导你完成所有配置。

### 使用

安装后直接对 Cola 说：

```
帮我连接钉钉
```

Cola 会自动：
1. 安装 dws CLI 工具（如果没装）
2. 打开浏览器进行钉钉授权登录
3. 验证连接状态
4. 提示你可以开始使用了

全程你只需要在浏览器里确认一次授权。

连接成功后，试试这些：
- "发消息到工作群"
- "我有什么待办"
- "明天有什么会"
- "帮我找一下张三"
- "查一下 AI 表格的数据"

### 反馈与问题

使用过程中遇到问题？Cola 会自动引导你提交反馈。你也可以直接前往：

- [提交 Issue](https://github.com/heran11011/cola-dingtalk-skills/issues/new)

常见问题：
- **dws 安装失败**：检查 Node.js 版本（需要 >= 18），或尝试 curl 安装方式
- **授权失败**：确认企业管理员已开通 CLI 访问权限
- **命令报错**：运行 `dws --version` 确认版本，附上错误信息提交 Issue

### 与飞书版的区别

| | Cola Lark Skills | Cola DingTalk Skills |
|---|---|---|
| CLI 工具 | lark-cli | dws |
| 文档搜索 | 支持 | dws 暂不支持 |
| 通讯录查询 | 无 | 支持 |
| 消息 | 读+写 | 仅发送（bot） |
| 认证方式 | 创建飞书应用 | 浏览器 OAuth |

---

## English

### Introduction

DingTalk integration skill pack for [Cola](https://cola.dev). After installation, use natural language to let Cola help you with DingTalk — send messages, check calendar, manage tasks, search contacts, and operate AI tables.

Built on DingTalk's official CLI tool [dws](https://github.com/nicepkg/dws) (dingtalk-workspace-cli), designed for AI Agents.

### Included Skills

| Skill | Function | Trigger Example |
|-------|----------|----------------|
| **dingtalk-setup** | DingTalk connection setup | "connect to DingTalk" |
| **dingtalk-messages** | Group messaging | "send message to DingTalk group" |
| **dingtalk-tasks** | Task management | "what are my tasks" |
| **dingtalk-calendar** | Calendar & schedule | "any meetings tomorrow" |
| **dingtalk-contacts** | Contact search | "find Zhang San" |
| **dingtalk-aitables** | AI table operations | "query data in the table" |

### Installation

#### Option 1: Quick Install (Recommended)

**macOS / Linux:**
```bash
git clone https://github.com/heran11011/cola-dingtalk-skills.git
cd cola-dingtalk-skills
chmod +x install.sh
./install.sh
```

**Windows:**
```cmd
git clone https://github.com/heran11011/cola-dingtalk-skills.git
cd cola-dingtalk-skills
install.bat
```

#### Option 2: Manual Install

Copy the 6 folders under `skills/` to Cola's skills directory:

| OS | Path |
|----|------|
| macOS / Linux | `~/.cola/mods/default/skills/` |
| Windows | `%USERPROFILE%\.cola\mods\default\skills\` |

### Prerequisites

- [Cola](https://cola.dev)
- [Node.js](https://nodejs.org) (needed for npm install of dws)

No need to install dws in advance — just tell Cola "connect to DingTalk" and it will guide you through the entire setup automatically.

### Usage

After installation, just tell Cola:

```
帮我连接钉钉
```

Cola will automatically:
1. Install the dws CLI tool (if not present)
2. Open browser for DingTalk OAuth login
3. Verify connection status
4. Let you know you're ready to go

You only need to confirm authorization once in the browser.

Once connected, try:
- "发消息到工作群" (send message to work group)
- "我有什么待办" (what are my tasks)
- "明天有什么会" (any meetings tomorrow)
- "帮我找一下张三" (find Zhang San)
- "查一下 AI 表格的数据" (query AI table data)

### Feedback & Issues

Having trouble? Cola will automatically guide you to submit feedback. You can also go directly to:

- [Submit an Issue](https://github.com/heran11011/cola-dingtalk-skills/issues/new)

Common issues:
- **dws install fails**: Check Node.js version (>= 18 required), or try the curl install method
- **Auth fails**: Confirm your organization admin has enabled CLI access
- **Command errors**: Run `dws --version` to check the version, include error output when submitting an Issue

### Compared to Lark Version

| | Cola Lark Skills | Cola DingTalk Skills |
|---|---|---|
| CLI Tool | lark-cli | dws |
| Doc Search | Supported | Not yet (dws roadmap) |
| Contact Search | No | Supported |
| Messaging | Read + Write | Send only (bot) |
| Auth Method | Create Lark app | Browser OAuth |

---

### 相关项目 / Related Projects

| 项目 | 说明 |
|------|------|
| [cola-lark-skills](https://github.com/heran11011/cola-lark-skills) | Cola 连接飞书，帮你操作飞书（Cola → 飞书） |
| [cola-feishu-bridge](https://github.com/heran11011/cola-feishu-bridge) | 在飞书中直接跟 Cola 对话（飞书 → Cola） |
| [cola-dingtalk-skills](https://github.com/heran11011/cola-dingtalk-skills)（本仓库） | Cola 连接钉钉，帮你操作钉钉（Cola → 钉钉） |

---

## ⚠️ 安全提示 / Security Notes

- **OAuth 授权**：连接钉钉时会打开浏览器授权页面，请确认 URL 为钉钉官方域名（`login.dingtalk.com`），不要在非官方页面输入密码
- **Token 过期**：如果遇到"权限不足"或"token expired"错误，重新执行 `dws auth login` 即可
- **消息发送确认**：所有发送消息的操作都会先让你确认内容，不会自动发送
- **输入安全**：本技能包通过 shell 命令与 dws CLI 交互，所有用户输入会经过转义处理
- **OAuth Security**: When connecting DingTalk, verify the browser URL is an official domain (`login.dingtalk.com`) before entering credentials
- **Token Expiry**: If you encounter "permission denied" or "token expired" errors, re-run `dws auth login`
- **Message Confirmation**: All message-sending operations require your explicit approval before sending
- **Input Safety**: This skill pack interacts with dws CLI via shell commands; all user inputs are sanitized

---

## License

MIT
