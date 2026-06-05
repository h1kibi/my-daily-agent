---
description: 用 Brave API 批量搜索并入库到本地知识库 kb
agent: build
model: aipie-cc/claude-opus-4-7
---

# /kb-collect - 批量采集命令

当用户说 `/kb-collect <主题>` 时，执行以下固定流程，不允许跳过任何步骤。

## 流程

### Step 1: 关键词扩展
根据用户给的主题，扩展中英文关键词。规则：
- 英文: 主题 + analysis, technical analysis, detection, mitigation, defense, exploit PoC, writeup, threat report, filetype:pdf, site:github.com, GitHub tool, Sigma YARA detection, CVE
- 中文: 主题 + 漏洞分析, 复现检测防御, 安全研究报告, 攻击路径, PoC利用, 检测规则

生成至少 10 个搜索关键词。

### Step 2: 执行本地采集脚本
```bash
cd <KB_WORKSPACE>
.\.venv\Scripts\python.exe .\scripts\collect_brave.py "<用户主题>" --min-candidates 100 --max-read 30 --max-save 18 --per-domain 8
```

### Step 3: 检查结果
列出 `<KB_ARTICLES_DIR>` 下新生成的文件。
检查 `<KB_LOG_DIR>` 下的失败日志。

### Step 4: 生成报告
告诉用户：
- 总共搜索了多少候选 URL
- 成功抓取多少篇
- 失败多少篇
- 保存到本地知识库的路径
- 生成的主题索引位置

### Step 5: 质量建议
如果某篇文章内容太少（<500字），建议用户手动补充或删除。
