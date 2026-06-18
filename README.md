# Ingest PDF RAG

A Retrieval-Augmented Generation (RAG) application that allows users to upload PDF documents and ask questions about their content.

The system uses an event-driven architecture powered by Inngest for workflow orchestration, observability, debugging, and function execution.

## Tech Stack

### AI & RAG

* Google Gemini API
* LlamaIndex (PDF Parsing, Chunking, Embeddings)
* Qdrant Vector Database using Docker

### Backend

* FastAPI
* Uvicorn
* Inngest (Orchestration)

### Frontend

* Streamlit

### Package Management

* uv

---

## Architecture

```text
PDF Upload
    │
    ▼
Inngest Event
    │
    ▼
LlamaIndex Processing
    │
    ├── PDF Parsing
    ├── Chunking
    └── Embedding Generation
    │
    ▼
Qdrant Vector Store


User Question
    │
    ▼
Inngest Event
    │
    ▼
Vector Search (Qdrant)
    │
    ▼
Context Retrieval
    │
    ▼
Google Gemini
    │
    ▼
Final Answer
```

---

## Environment Variables

Create a `.env` file:

```env
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL_NAME=model_name
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/OmkarTanajiPatil/Ingest_PDF_RAG.git
cd Ingest_PDF_RAG
```

Install dependencies:

```bash
uv sync
```

---

## Running the Project

### 1. Start Qdrant

```bash
docker run -d \
  --name qdrant \
  -p 6333:6333 \
  -v "$(pwd)/qdrant_storage:/qdrant/storage" \
  qdrant/qdrant
```

### 2. Start FastAPI Backend

```bash
uv run uvicorn main:app
```

### 3. Start Inngest Dev Server

```bash
npx inngest-cli@latest dev -u http://127.0.0.1:8000/api/inngest --no-discovery
```

### 4. Start Streamlit UI

```bash
uv run streamlit run streamlitapp.py
```

---

## Usage

1. Upload a PDF through the Streamlit interface.
2. The ingestion workflow is triggered through Inngest.
3. PDF content is parsed and chunked using LlamaIndex.
4. Embeddings are generated and stored in Qdrant.
5. Ask questions about the uploaded document.
6. Relevant context is retrieved from Qdrant.
7. Google Gemini generates the final response.
