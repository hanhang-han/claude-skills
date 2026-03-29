# Error Journal

[中文](#中文) | [English](#english)

---

## 中文

### 概述

Error Journal 是一个 Claude Code 技能，用于自动记录执行 bash 命令时遇到的错误，形成可检索的错误知识库，帮助你积累经验、避免重复犯错。

### 安装

```bash
npx skills add hanhang-han/claude-skills@error-journal -g -y
```

### 功能特点

- **自动触发**：当 bash 命令执行失败（返回非零退出码）时自动记录
- **手动触发**：说 "记下来这个错误"、"这个坑要记住"、"记录错误" 时记录
- **历史查询**：问 "有没有遇到过..." 时搜索历史错误

### 使用方法

#### 自动记录
当命令失败时，技能会自动记录错误信息：
```
[执行命令]
docker-compose up -d

[错误]
Error: port 80 already in use

[自动记录到错误日志]
```

#### 手动记录
```
用户: 这个坑要记住，npm install 时要用 --legacy-peer-deps

[Claude 自动记录]
```

#### 查询历史
```
用户: 之前遇到过端口占用的问题吗？

[Claude 搜索错误日志并返回相关记录]
```

### 错误日志位置

```
~/.claude/skills/error-journal/references/error-log.md
```

### 记录格式

| 字段 | 说明 |
|------|------|
| 日期 | YYYY-MM-DD HH:MM |
| 命令 | 执行的命令 |
| 错误 | 错误信息摘要 |
| 上下文 | 当时在做什么 |
| 根因 | 为什么出错 |
| 方案 | 如何解决的 |
| 教训 | 以后如何避免 |

---

## English

### Overview

Error Journal is a Claude Code skill that automatically logs errors encountered during bash command execution, building a searchable knowledge base of mistakes and lessons learned to prevent repeated errors.

### Installation

```bash
npx skills add hanhang-han/claude-skills@error-journal -g -y
```

### Features

- **Auto-trigger**: Automatically logs when a bash command fails (returns non-zero exit code)
- **Manual trigger**: Logs when you say "log this error", "remember this", "note this mistake"
- **History query**: Searches past errors when you ask "have we seen..."

### Usage

#### Auto Logging
When a command fails, the skill automatically logs the error:
```
[Command executed]
docker-compose up -d

[Error]
Error: port 80 already in use

[Auto-logged to error journal]
```

#### Manual Logging
```
User: Remember this - npm install needs --legacy-peer-deps

[Claude automatically logs]
```

#### Query History
```
User: Have we seen port conflicts before?

[Claude searches error log and returns matching records]
```

### Error Log Location

```
~/.claude/skills/error-journal/references/error-log.md
```

### Record Format

| Field | Description |
|-------|-------------|
| Date | YYYY-MM-DD HH:MM |
| Command | The command executed |
| Error | Error message summary |
| Context | What task was being done |
| Root Cause | Why it happened |
| Solution | How it was fixed |
| Lesson | How to avoid in the future |

---

## License

MIT
