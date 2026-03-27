# TextRag — English Text RAG Example

This project demonstrates a complete RAG (Retrieval-Augmented Generation) pipeline, including text chunking, vector embedding, vector retrieval, Cross-Encoder reranking, and answer generation using Google Gemini.

## Tech Stack

| Component | Description |
|-----------|-------------|
| [sentence-transformers](https://www.sbert.net/) | Text vector embeddings (`all-MiniLM-L6-v2`) |
| [ChromaDB](https://www.trychroma.com/) | Lightweight local vector database |
| Cross-Encoder | Retrieval reranking (`cross-encoder/ms-marco-MiniLM-L-6-v2`) |
| [Google Gemini](https://ai.google.dev/) | LLM answer generation (`gemini-2.5-flash`) |
| [UV](https://docs.astral.sh/uv/) | Python package management |

---

## Requirements

- Python **3.12 or 3.13** (3.14 is not supported due to `onnxruntime` compatibility)
- [UV](https://docs.astral.sh/uv/) package manager
- Google AI Studio API Key

---

## Installation

### 1. Install UV

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Clone the repository and navigate to the directory

```bash
git clone <repository-url>
cd TextRag/EN_example
```

### 3. Install Python 3.13 and sync dependencies

```bash
uv python install 3.13
uv sync --python 3.13
```

### 4. Configure API Key

Create a `.env` file in the project root (`TextRag/`):

```bash
GOOGLE_API_KEY=your_google_api_key_here
```

> You can obtain a free API Key at [Google AI Studio](https://aistudio.google.com/apikey).

---

## Running the Project

Launch Jupyter Notebook from the `EN_example/` directory:

```bash
uv run jupyter notebook
```

Then open `en_rag.ipynb` in your browser and run the cells in order.

---

## Pipeline Overview

```
Document (doc.md)
    ↓ Split into paragraphs
Text chunks
    ↓ Embed with sentence-transformers
Store vectors in ChromaDB
    ↓ User query → top-k vector retrieval
Candidate chunks
    ↓ Cross-Encoder reranking
Top-ranked chunks
    ↓ Assemble as Prompt → Gemini generates
Final answer
```

---

## Project Structure

```
TextRag/
├── .env                  # API Key (never commit to Git)
├── .gitignore
├── README.md
└── EN_example/
    ├── en_rag.ipynb      # Main notebook
    ├── doc.md            # Sample document
    ├── pyproject.toml    # Project dependencies
    └── uv.lock           # Dependency lockfile
```
