# AI Learning Tutor — 项目配置

## 项目简介

这是一个 AI 初学者自学辅助项目。通过自动抓取 AI 大厂最新博客，生成结构化的深度精读笔记，存入 Obsidian Vault 建立个人 AI 知识库。

## 可用 Task

### `ai-tutor` — AI 前沿精读

> 触发方式：在对话中直接说 "运行 ai-tutor" 或 "/ai-tutor"

**功能：** 抓取 AI 大厂最新博客，生成一篇面向初学者的精读笔记，自动存入 Obsidian Vault。

**默认来源：** Anthropic Engineering (`https://www.anthropic.com/engineering`)

**切换来源（通过参数）：**
- `/ai-tutor` — Anthropic Engineering（默认）
- `/ai-tutor openai` — OpenAI Blog
- `/ai-tutor cursor` — Cursor Blog

**生成笔记包含：**
1. 📌 概览信息（标题、来源、日期、链接）
2. 💡 术语百科（≥3 个专业术语通俗解释）
3. 🚀 前沿速递（本文核心发布内容）
4. 🛠️ 核心原理解析（含关键图表 + Claude 导读）
5. 🧠 学习重点（3 个 Takeaways）
6. 🔍 关联思考（与已有笔记建立 Obsidian 知识图谱连接）
7. 📰 简报区（其他来源今日动态）

**输出路径：** `<VAULT_ROOT>/AI_Learning/YYYY-MM-DD-标题.md`

**图片：** 关键图表自动下载到 `<VAULT_ROOT>/attachments/`

**已读追踪：** 自动维护 `<VAULT_ROOT>/.ai-tutor-read-log.md`，避免重复处理。若当日来源无新文章，自动读取最近未读的旧文章。

## 前置条件

- defuddle-cli 已安装：`npm install -g defuddle-cli`
- MCP fetch 已配置（用于 fallback）
- MCP obsidian-vault 已配置，挂载你的 Obsidian Vault 根目录

## 配置

使用前请在 `ai-tutor/SKILL.md` 的"Vault 路径配置"部分，将 `<VAULT_ROOT>` 替换为你本地的 Obsidian Vault 绝对路径，例如：

```
/Users/你的用户名/Documents/Obsidian-Vault/
```

## 注意事项

- `AI_Learning/` 目录不存在时需先创建
- Skill 定义文件位于：`~/.claude/skills/ai-tutor/SKILL.md`
