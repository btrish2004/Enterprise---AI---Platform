**Enterprise AI Knowledge Platform**

A secure, multi-tenant enterprise RAG platform for intelligent document question answering. The platform combines role-based access control, document versioning, semantic retrieval, cross-encoder reranking, relevance filtering, and local LLM generation to provide context-grounded answers with source citations.

**Architecture**

                         Enterprise AI Knowledge Platform
                                      │
                         ┌────────────┴────────────┐
                         │                         │
                  JWT Authentication       Multi-Tenancy
                         │                         │
                         └────────────┬────────────┘
                                      ↓
                             Document Management
                                      │
                         Versioning + Metadata
                                      ↓
                               Document Ingestion
                            PDF / DOCX / TXT
                                      ↓
                              Structure-Aware
                                  Chunking
                                      ↓
                              BGE Embeddings
                                      ↓
                              Qdrant Vector DB
                                      ↓
                         Tenant-Filtered Retrieval
                                      ↓
                         Cross-Encoder Reranking
                                      ↓
                              Relevance Guard
                                      ↓
                         Qwen 2.5 Local LLM
                                      ↓
                          Answer + Source Citations

**Key Features**

Enterprise Security

Multi-tenant architecture

JWT-based authentication

Role-based access control (Admin / Member / Viewer)

Tenant-isolated document retrieval

Protected document operations

Document Intelligence

PDF, DOCX, and TXT document ingestion

Document versioning

Structure-aware chunking

Metadata and page-level tracking

Retrieval-Augmented Generation

BGE embeddings for semantic search

Qdrant vector database

Tenant-filtered vector retrieval

Cross-encoder reranking

Relevance threshold to prevent unsupported answers

Context-grounded local LLM generation

Source and page-level citations

**Engineering**

FastAPI REST APIs

PostgreSQL persistence

Alembic database migrations

Dockerized infrastructure

Automated tests

Local LLM inference using Hugging Face

**Enterprise Use Cases**

The platform can serve as an internal enterprise knowledge assistant for retrieving information from policies, procedures, standard operating procedures, and business documentation.

**HR & Employee Policies**

What is the company's parental leave policy?

How many days of annual leave can be carried forward?

What is the process for requesting remote work?

What are the eligibility criteria for employee reimbursements?

**Finance & Procurement**

What is the approval process for expenses above $5,000?

Which expenses require manager approval?

What is the process for creating a purchase order?

Which vendors are approved for a specific category?

**IT & Security**

How do I request access to an internal application?

What is the procedure for reporting a security incident?

What are the requirements for accessing company data remotely?

What is the process for requesting privileged access?

**Operations & Business Processes**

What are the steps for onboarding a new employee?

What is the standard operating procedure for this process?

Who is responsible for approving this request?

What is the escalation procedure for an operational issue?

**Example RAG Workflow**

**Question**

**What is the current approval process for expenses above $5,000, and which document and page describe it?**

Processing Pipeline

Authenticate the user using JWT

Identify the user's tenant and permissions

Retrieve relevant document chunks

Apply tenant-level filtering

Rerank retrieved passages using a cross-encoder

Apply a relevance threshold

Generate an answer using only the retrieved context

Return supporting document and page references

This approach helps keep responses grounded in the organization's internal knowledge base rather than relying on unsupported information.

Example

Question

What is the policy for working overtime?

Answer

Overtime should generally be worked only when there is a genuine business requirement and, where applicable, with prior approval from your manager. You must accurately record all overtime hours in the designated timekeeping or HR system.
Whether you are eligible for overtime compensation or time off in lieu depends on your role, employment terms, applicable company policies, and local labor laws. Employees should not work overtime that is unapproved or unrecorded.

Sources

Document: Company_policies.pdf
Page: 1
Relevance Score: 1.0

The system retrieves the relevant document chunks, reranks them, passes the highest-relevance context to the local LLM, and returns the generated answer together with its supporting sources.

**Relevance Guard**

The platform does not blindly generate an answer for every query.

For questions where relevant information cannot be found in the tenant's document collection, the system returns:

I couldn't find this information in the provided documents.

This prevents the LLM from generating answers when sufficient retrieved context is unavailable.

**Security**

The platform implements multiple layers of isolation:

JWT authentication

Role-based authorization

Tenant isolation

Tenant-filtered vector search

Tenant-scoped document operations

Protected upload and indexing endpoints

**Tech Stack**

Python

API

FastAPI

Database

PostgreSQL

Vector Database

Qdrant

Embeddings

BAAI/bge-small-en-v1.5

Reranker

BAAI/bge-reranker-base

LLM

Qwen 2.5 Instruct

ORM

SQLAlchemy

Migrations

Alembic

Authentication

JWT

Infrastructure

Docker

Testing

Pytest

ML Framework

Hugging Face / Sentence Transformers


**Open API documentation
**
http://127.0.0.1:8000/docs

The project includes tests covering document extraction, chunking, embeddings, authentication/security, and core application functionality.
