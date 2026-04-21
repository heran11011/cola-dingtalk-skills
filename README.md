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

### Compared to Lark Version

| | Cola Lark Skills | Cola DingTalk Skills |
|---|---|---|
| CLI Tool | lark-cli | dws |
| Doc Search | Supported | Not yet (dws roadmap) |
| Contact Search | No | Supported |
| Messaging | Read + Write | Send only (bot) |
| Auth Method | Create Lark app | Browser OAuth |

---

## License

MIT
