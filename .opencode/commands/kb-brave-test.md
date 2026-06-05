---
description: 测试 Brave API Key、Brave MCP、本地知识库采集脚本是否正常
agent: build
---

# /kb-brave-test - 测试 Brave 集成

执行以下测试：

### Test 1: 环境变量
```bash
powershell -Command "[Environment]::GetEnvironmentVariable('BRAVE_API_KEY','User') -replace '^(.).*','$1***'"
```

### Test 2: Brave API 直连
```bash
$key = [Environment]::GetEnvironmentVariable("BRAVE_API_KEY", "User")
curl.exe "https://api.search.brave.com/res/v1/web/search?q=test" -H "Accept: application/json" -H "X-Subscription-Token: $key" | Select-String "web"
```

### Test 3: 采集脚本
```bash
cd <KB_WORKSPACE>
.\.venv\Scripts\python.exe .\scripts\collect_brave.py "测试" --min-candidates 5 --max-read 2 --max-save 1 --per-domain 1
```

### Test 4: 本地检索
```bash
cd <KB_WORKSPACE>
.\.venv\Scripts\python.exe .\scripts\search_kb_text.py "测试"
```

报告每项测试结果。
