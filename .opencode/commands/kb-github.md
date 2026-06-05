---
description: 研究 GitHub 项目（只读），提取关键信息写入本地知识库
agent: build
---

# /kb-github - GitHub 研究命令

使用 GitHub MCP（只读模式）研究指定项目。

## 前置条件
确保 GitHub MCP 已启用：
```bash
opencode mcp enable github
```

## 流程

### Step 1: 获取仓库信息
使用 GitHub MCP 获取项目的 README、最近 commits、issues、PRs。

### Step 2: 分析代码结构
检查项目的目录结构、关键文件、依赖。

### Step 3: 提取可用信息
- 项目用途和核心功能
- 安装和配置步骤
- 与知识库研究的关联
- 可复用的技术点

### Step 4: 写入本地知识库
将分析结果写入本地知识库 Markdown 目录，格式同其他采集文章。

### Step 5: 任务完成后关闭 GitHub MCP
```bash
opencode mcp disable github
```
