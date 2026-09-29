# Enterprise AI Knowledge Platform

A multi-tenant enterprise RAG platform for secure document
question answering with role-based access control, vector
retrieval, reranking, relevance filtering, and local LLM generation.

## Architecture

User
 ↓
JWT Authentication
 ↓
RBAC + Multi-Tenancy
 ↓
Document Upload
 ↓
PDF / DOCX / TXT Extraction
 ↓
Semantic Chunking
 ↓
BGE Embeddings
 ↓
Qdrant Vector Database
 ↓
Tenant-Filtered Retrieval
 ↓
Cross-Encoder Reranking
 ↓
Relevance Guard
 ↓
Qwen Local LLM
 ↓
Answer + Sources

## Key Features

- Multi-tenant architecture
- JWT authentication
- Role-based access control
- Document versioning
- PDF, DOCX and TXT ingestion
- Structure-aware document chunking
- BGE embeddings
- Qdrant vector search
- Tenant-isolated retrieval
- Cross-encoder reranking
- Relevance threshold / hallucination prevention
- Local LLM inference using Hugging Face
- Source citations
- Dockerized infrastructure
- Automated tests

## Tech Stack

Python
FastAPI
PostgreSQL
Qdrant
Sentence Transformers
BGE Embeddings
BGE Reranker
Qwen 2.5
Docker
Alembic
JWT
Pytest

## Example

Question:

"When did Manmohan Singh serve as Prime Minister of India?"

The system retrieves relevant document chunks, reranks them,
passes the relevant context to the local LLM, and returns an
answer together with document and page-level sources.

## Security

The platform implements:

- JWT authentication
- Role-based authorization
- Tenant isolation
- Tenant-filtered vector retrieval
- Protected document operations

## Running Locally

```bash
docker compose up -d

cd backend

uvicorn app.main:app --reload
