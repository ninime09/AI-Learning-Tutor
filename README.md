# 🤖 AI Tutor — Claude Code Skill

一个面向 AI 初学者的 Claude Code Skill，自动抓取 Anthropic、OpenAI、Cursor 等大厂最新博客，生成结构化深度精读笔记，直接存入你的 Obsidian Vault。

---

## ✨ 功能亮点

- **智能内容提取**：优先使用 defuddle 提取干净正文，自动过滤广告和导航栏
- **递进式笔记结构**：从术语解释到原理剖析，专为零基础学习者设计
- **关键图表下载**：Claude 自动识别架构图、流程图等关键图表并本地化
- **知识图谱连接**：自动扫描已有笔记，用 Obsidian wikilink 建立知识关联
- **已读追踪**：自动记录已读文章，下次运行自动跳过，支持读取历史旧文章
- **行业简报**：每次附上其他来源的最新动态标题

## 📄 生成笔记结构

```
📌 核心速递      → 一句话说清楚这篇文章讲了什么
💡 术语百科      → ≥3 个专业术语的大白话解释
🚀 前沿速递      → 本文核心发布内容（新模型/新功能/新研究）
🛠️ 核心原理解析  → 现象→背景→原理→意义，含关键图表 + Claude 导读
🧠 学习重点      → 3 个初学者最应带走的 Takeaways
🔍 关联思考      → 与 Obsidian 知识库中已有笔记的连接
📰 简报区        → 其他来源今日最新动态
```

---

## 🚀 安装方法

### 前置条件

```bash
# 1. 安装 defuddle-cli（内容提取工具）
npm install -g defuddle-cli

# 2. 确保 Claude Code 已安装
# https://claude.ai/download
```

在 `~/.claude/settings.json` 中配置两个 MCP 服务器：

```json
{
  "mcpServers": {
    "fetch": {
      "command": "mcp-server-fetch"
    },
    "obsidian-vault": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/你的/Obsidian/Vault/路径"]
    }
  }
}
```

### 安装 Skill

将 `ai-tutor` 文件夹复制到 Claude Code 的 skills 目录：

```bash
# macOS / Linux
cp -r ai-tutor ~/.claude/skills/

# 验证安装
ls ~/.claude/skills/ai-tutor/
# 应输出：SKILL.md
```

### 配置 Vault 路径

打开 `~/.claude/skills/ai-tutor/SKILL.md`，找到"Vault 路径配置"部分，将路径替换为你自己的 Obsidian Vault 路径：

```
vault_root:    /你的用户名/Documents/Obsidian-Vault/
notes_dir:     AI_Learning/
attachments:   attachments/
read_log:      .ai-tutor-read-log.md
```

---

## 📖 使用方法

在 Claude Code 中，进入你的项目目录，直接运行：

```bash
# 读取 Anthropic Engineering 最新文章（默认）
/ai-tutor

# 读取 OpenAI Blog 最新文章
/ai-tutor openai

# 读取 Cursor Blog 最新文章
/ai-tutor cursor
```

运行后，笔记自动保存到你的 Obsidian Vault：

```
Obsidian-Vault/
├── AI_Learning/
│   └── 2026-03-02-文章标题.md    ← 生成的精读笔记
├── attachments/
│   └── 2026-03-02-anthropic-架构图.png  ← 下载的关键图表
└── .ai-tutor-read-log.md          ← 已读记录（自动维护）
```

---

## 📁 文件结构

```
ai-tutor/
└── SKILL.md    # Skill 定义文件，包含完整工作流程
```

---

## 🛠️ 支持的来源

| 来源 | 参数 | URL |
|------|------|-----|
| Anthropic Engineering | 默认 | https://www.anthropic.com/engineering |
| OpenAI Blog | `openai` | https://openai.com/news |
| Cursor Blog | `cursor` | https://www.cursor.com/blog |

欢迎提 PR 添加更多来源！

---

## 📋 依赖

| 工具 | 用途 | 安装方式 |
|------|------|----------|
| [Claude Code](https://claude.ai/download) | 运行环境 | 官网下载 |
| [defuddle-cli](https://github.com/kepano/defuddle) | 网页内容提取 | `npm install -g defuddle-cli` |
| mcp-server-fetch | 网页抓取 fallback | `pip install mcp-server-fetch` |
| @modelcontextprotocol/server-filesystem | Obsidian Vault 读写 | 配置 MCP 时自动安装 |

---

## 🤝 贡献

欢迎通过 Issue 或 PR 改进这个 Skill：
- 添加新的博客来源
- 优化笔记结构
- 改进术语提取逻辑
- 支持更多语言
