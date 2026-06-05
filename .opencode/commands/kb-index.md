---
description: 将 Obsidian SecKB 文章写入 Chroma 向量索引
agent: build
---

# /kb-index - 向量索引命令

将知识库 Markdown 文章写入 Chroma 向量数据库。

## 流程

### Step 1: 检查 Chroma 环境
```bash
cd <SECKB_WORKSPACE>
.\.venv\Scripts\python.exe -c "import chromadb; print('ChromaDB ready:', chromadb.__version__)"
```

### Step 2: 执行索引脚本
请根据本机路径替换以下占位符：
- `<OBSIDIAN_SECKB>`
- `<CHROMA_DB_PATH>`

```bash
cd <SECKB_WORKSPACE>
.\.venv\Scripts\python.exe -c "
import os, frontmatter
from pathlib import Path
from chromadb import PersistentClient
from chromadb.utils import embedding_functions

articles = Path('<OBSIDIAN_SECKB>').glob('*.md')
client = PersistentClient(path='<CHROMA_DB_PATH>')
ef = embedding_functions.SentenceTransformerEmbeddingFunction(model_name='all-MiniLM-L6-v2')

try:
    client.delete_collection('seckb_articles')
except:
    pass

collection = client.create_collection('seckb_articles', embedding_function=ef)
count = 0
for f in articles:
    fm_data = frontmatter.load(f)
    title = fm_data.get('title', f.stem)
    content = fm_data.content[:8000]
    collection.add(
        documents=[content],
        metadatas=[{'title': title, 'source': fm_data.get('source',''), 'file': str(f)}],
        ids=[f.stem]
    )
    count += 1
print(f'Indexed {count} articles')
"
```

### Step 3: 报告
- 索引了多少篇文章
- Chroma 数据库路径
