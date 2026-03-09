# RAG Automation – Google Drive FAQ Bot (n8n + Gemini + Pinecone)

## Overview

This project demonstrates an automated Retrieval-Augmented Generation (RAG) pipeline built using **n8n**, **Google Gemini**, and **Pinecone**.

The workflow automatically ingests documents from a Google Drive folder, converts them into vector embeddings, stores them in a vector database, and allows users to query the knowledge base through an AI agent.

The system enables dynamic question answering over uploaded documents such as policies, FAQs, and knowledge base files.

---

## Architecture

Document Ingestion Pipeline:

Google Drive Folder
→ File Trigger
→ File Download
→ Text Chunking
→ Gemini Embeddings
→ Pinecone Vector Database
## Architecture Diagram
<img width="1536" height="1024" alt="architecture png" src="https://github.com/user-attachments/assets/913c7cef-9c8a-4d5d-a89e-2528711c2cda" />

Query Pipeline:

User Chat Message
→ AI Agent
→ Pinecone Retriever Tool
→ Gemini LLM
→ Final Answer

---

## Workflow Explanation

### 1. Google Drive Trigger

The workflow monitors a specific Google Drive folder for new documents.

When a new file is uploaded:

* The workflow automatically triggers.

### 2. File Download

The file is downloaded from Google Drive for processing.

### 3. Document Loader

The document is parsed and prepared for text extraction.

### 4. Text Splitting

The document is split into smaller chunks using **Recursive Character Text Splitter** to improve retrieval accuracy.

### 5. Embedding Generation

Each text chunk is converted into vector embeddings using:

Gemini Model:
models/gemini-embedding-001

Vector dimension: 3072

### 6. Vector Storage

The embeddings are stored inside **Pinecone Vector Database** under a namespace.

Index configuration:

* Index name: google
* Dimension: 3072
* Metric: cosine

---

## AI Query System

### Chat Trigger

A user sends a query through the chat interface.

### AI Agent

The agent processes the query and decides whether to call the retrieval tool.

### Pinecone Retriever

The Pinecone vector store is exposed as a tool for the agent.

The agent retrieves the most relevant document chunks.

### Gemini LLM

The retrieved context is passed to **Gemini Flash model** to generate the final answer.

---

## Technologies Used

* n8n (Workflow Automation)
* Google Gemini API
* Pinecone Vector Database
* Google Drive API
* Retrieval-Augmented Generation (RAG)

---

## Key Features

* Automated document ingestion
* Semantic vector search
* AI agent-based retrieval
* Real-time document updates
* Fully serverless architecture

---

## Use Cases

* FAQ chatbot
* Policy assistant
* Knowledge base search
* Internal documentation assistant

---

## Setup Instructions

1. Clone this repository
2. Import the n8n workflow JSON
3. Configure credentials:

   * Google Drive API
   * Gemini API
   * Pinecone API
4. Create Pinecone index with dimension **3072**
5. Upload documents to the configured Google Drive folder

The system will automatically index documents and allow chat-based retrieval.

---

## Future Improvements

* Add conversation memory
* Implement hybrid search
* Add document metadata filtering
* Deploy as a public chatbot interface
