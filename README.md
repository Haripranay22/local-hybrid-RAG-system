# Local Hybrid RAG System (OpenSearch + Ollama)

A fully local **Hybrid Retrieval-Augmented Generation (RAG)** system that combines
**semantic vector search + keyword search** using **OpenSearch**, and generates
responses using **Ollama-hosted LLMs**, wrapped in an interactive **Streamlit UI**.

This project demonstrates how to build a **production-style, local-first RAG pipeline**
without relying on external cloud LLM APIs.

---

## 🚀 Features

- 🔍 **Hybrid Search**
  - Dense vector search (Sentence Transformers embeddings)
  - Sparse keyword search (BM25)
  - Combined relevance scoring using OpenSearch

- 🤖 **Local LLM Inference**
  - Uses **Ollama** (e.g. `llama3:latest`)
  - No OpenAI / cloud dependency

- 📄 **Document Ingestion**
  - Upload PDFs
  - Chunking + embedding
  - Indexed into OpenSearch

- 🧠 **RAG Mode Toggle**
  - Enable / disable RAG at query time
  - Adjustable context window size

- 🖥️ **Streamlit UI**
  - Chat interface
  - Upload documents
  - Temperature control
  - Search result tuning

---

## 🧠 Architecture Overview
This project implements a **local, hybrid Retrieval-Augmented Generation (RAG) architecture** that combines semantic vector search with keyword-based retrieval, followed by local LLM inference.    
User Query
│
▼
Streamlit UI
│
▼
Query Embedding
(SentenceTransformer)
│
▼
Hybrid Retrieval (OpenSearch)
├── Dense Vector Search (kNN)
└── Sparse Keyword Search (BM25)
│
▼
Top-K Relevant Context Chunks
│
▼
Prompt Construction
│
▼
Ollama (Local LLM - llama3)
│
▼
Final Answer

### Component Breakdown

- **Streamlit UI**
  - Handles user interaction, document uploads, and configuration controls.

- **Embedding Layer**
  - Converts user queries and document chunks into dense vector representations using Sentence Transformers.

- **OpenSearch Hybrid Retrieval**
  - Performs:
    - kNN vector similarity search for semantic relevance
    - BM25 keyword search for exact term matching
  - Combines both signals to retrieve the most relevant context.

- **Context Window Builder**
  - Selects top-k retrieved chunks and formats them into a structured prompt.

- **Ollama LLM**
  - Runs a fully local LLM (`llama3`) to generate grounded responses based on retrieved context.

- **Response Generation**
  - Produces final answers with reduced hallucination by grounding responses in retrieved documents.

---

This architecture enables **cloud-free, privacy-preserving, and production-style RAG workflows** entirely on a local machine.


---

## 🧩 Tech Stack

| Layer | Technology |
|-----|-----------|
| UI | Streamlit |
| LLM | Ollama (`llama3`) |
| Search Engine | OpenSearch |
| Embeddings | `sentence-transformers/all-mpnet-base-v2` |
| Language | Python 3.12 |
| OS Support | Linux / WSL |

---

## 📂 Project Structure

```text
local-hybrid-RAG-system/
├── Welcome.py               # Streamlit entry point
├── pages/                   # UI pages (Chatbot, Upload)
├── src/                     # Core RAG logic
│   ├── chat.py
│   ├── embeddings.py
│   ├── opensearch_client.py
│   └── constants.py
├── notebooks/               # Experiments & exploration
├── images/                  # UI screenshots
├── requirements.txt
├── pyproject.toml
├── README.md
├── .gitignore
└── LICENSE

## ⚙️ Setup Instructions

### 1️⃣ Clone the repository
```bash
git clone https://github.com/Haripranay22/local-hybrid-RAG-system.git
cd local-hybrid-RAG-system

### 2️⃣ Create virtual environment
```bash
python3 -m venv .venv
source .venv/bin/activate

