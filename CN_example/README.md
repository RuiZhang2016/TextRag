# TextRag —— 中文文本 RAG 示例

本项目演示了一个完整的中文 RAG（检索增强生成）Pipeline，包含文本分块、向量嵌入、向量检索、Cross-Encoder 重排序，以及调用 Google Gemini 生成最终答案。

## 技术栈

| 组件 | 说明 |
|------|------|
| [sentence-transformers](https://www.sbert.net/) | 中文向量嵌入（`shibing624/text2vec-base-chinese`） |
| [ChromaDB](https://www.trychroma.com/) | 轻量级本地向量数据库 |
| Cross-Encoder | 检索结果重排序（`cross-encoder/mmarco-mMiniLMv2-L12-H384-v1`） |
| [Google Gemini](https://ai.google.dev/) | 大语言模型生成答案（`gemini-2.5-flash`） |
| [UV](https://docs.astral.sh/uv/) | Python 包管理 |

---

## 环境要求

- Python **3.12 或 3.13**（不支持 3.14，受 `onnxruntime` 限制）
- [UV](https://docs.astral.sh/uv/) 包管理器
- Google AI Studio API Key

---

## 安装步骤

### 1. 安装 UV

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. 克隆项目并进入目录

```bash
git clone <仓库地址>
cd TextRag/CN_example
```

### 3. 安装 Python 3.13 并同步依赖

```bash
uv python install 3.13
uv sync --python 3.13
```

### 4. 配置 API Key

在项目根目录（`TextRag/`）创建 `.env` 文件：

```bash
GOOGLE_API_KEY=your_google_api_key_here
```

> 可在 [Google AI Studio](https://aistudio.google.com/apikey) 免费获取 API Key。

---

## 运行方式

在 `CN_example/` 目录下启动 Jupyter Notebook：

```bash
uv run jupyter notebook
```

然后在浏览器中打开 `cn_rag.ipynb`，按顺序执行每个单元格即可。

---

## Pipeline 流程

```
文档（doc.md）
    ↓ 按段落分块
文本块（chunks）
    ↓ sentence-transformers 向量化
向量存入 ChromaDB
    ↓ 用户提问 → 向量检索 top-k
候选文本块
    ↓ Cross-Encoder 重排序
精选文本块
    ↓ 拼接为 Prompt → Gemini 生成
最终回答
```

---

## 目录结构

```
TextRag/
├── .env                  # API Key（不提交到 Git）
├── .gitignore
├── README.md
└── CN_example/
    ├── cn_rag.ipynb      # 主 Notebook
    ├── doc.md            # 示例文档（哆啦A梦故事）
    ├── pyproject.toml    # 项目依赖配置
    └── uv.lock           # 依赖锁定文件
```
