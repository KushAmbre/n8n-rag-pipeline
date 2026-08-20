# Automated RAG Knowledge Base & Chatbot Pipeline (n8n + Pinecone)

An end-to-end, event-driven Retrieval-Augmented Generation (RAG) system built with **n8n**, **OpenAI**, and **Pinecone**. This architecture decouples automated document indexing from conversational retrieval to deliver context-grounded responses in real time.

---

## 🏗️ Architecture Overview

The system is separated into two modular workflows:

### 1. Document Ingestion & Indexing Pipeline
![Ingestion Pipeline](/ingestion-workflow.png.png)
* **Trigger:** Listens for newly uploaded files in a target Google Drive folder via `Google Drive Trigger`.
* **Processing:** Downloads files and passes them to a `Default Data Loader` using `Recursive Character Text Splitter` for optimal chunking and overlap.
* **Vectorization & Storage:** Embeds text chunks via `Embeddings OpenAI` (`text-embedding-3-small`) and upserts them directly into a `Pinecone Vector Store` index.

### 2. Conversational Retrieval & Generation Pipeline
![Chat Retrieval Pipeline](/chat-workflow.png.png)
* **Trigger:** Captures user queries via `When chat message received`.
* **Retrieval:** Converts incoming user queries into embeddings to perform similarity search against Pinecone via `Vector Store Retriever`.
* **Response Generation:** Injects relevant document chunks into the prompt context and queries the `OpenAI Chat Model` via the `Question and Answer Chain` to return grounded, hallucination-free answers.
---

## 🛠️ Tech Stack

* **Orchestration:** n8n (Node-based workflow automation)
* **LLM & Embeddings:** OpenAI (`gpt-4o-mini` / `gpt-3.5-turbo`, OpenAI Embeddings)
* **Vector Database:** Pinecone
* **Data Sources:** Google Drive API
* **Chunking Strategy:** LangChain Recursive Character Text Splitting

---

## 🚀 Setup & Deployment

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/KushAmbre/n8n-rag-pipeline.git](https://github.com/KushAmbre/n8n-rag-pipeline.git)
   cd n8n-rag-pipeline
