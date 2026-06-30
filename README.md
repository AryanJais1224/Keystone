# Keystone

> **A GraphRAG platform that augments semantic retrieval with knowledge graph traversal, event-driven orchestration, and automated evaluation for fast, citation-grounded question answering.**

![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-Async%20API-green.svg)
![LangGraph](https://img.shields.io/badge/LangGraph-Orchestration-orange.svg)
![Neo4j](https://img.shields.io/badge/Neo4j-Knowledge%20Graph-008CC1.svg)
![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20DB-purple.svg)
![Redis](https://img.shields.io/badge/Redis-Semantic%20Cache-red.svg)
![Apache Kafka](https://img.shields.io/badge/Apache-Kafka-black.svg)
![License](https://img.shields.io/badge/License-MIT-success)

---

## Table of Contents

- [Overview](#overview)
- [Application User Interface](#application-user-interface)
- [Demo Video](#demo-video)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Retrieval Pipeline](#retrieval-pipeline)
- [Performance Benchmarks](#performance-benchmarks)
- [Engineering Decisions](#engineering-decisions)
- [Installation & Running the Project](#installation--running-the-project)
- [License](#license)
- [Author](#author)

---

# Overview

Keystone is a GraphRAG platform designed to answer complex questions over large collections of unstructured documents by combining semantic retrieval, knowledge graph traversal, and LLM-based response synthesis within an event-driven architecture.

Traditional Retrieval-Augmented Generation (RAG) systems rely solely on vector similarity search, often missing relationships that span multiple documents. Keystone augments retrieval by constructing a Neo4j knowledge graph alongside a vector index, allowing the system to combine semantic similarity with explicit entity relationships before generating responses.

To improve scalability and responsiveness, the platform incorporates Redis-backed semantic caching, asynchronous Kafka workers for document ingestion and evaluation, and a LangGraph orchestration pipeline that coordinates retrieval, graph expansion, response generation, and citation validation.

Beyond retrieval, Keystone includes an automated evaluation framework built around a Golden Dataset for measuring response faithfulness and relevance, enabling systematic benchmarking and regression testing as retrieval pipelines evolve.

### Core Engineering Objectives

- Build a hybrid GraphRAG pipeline combining vector search and knowledge graph traversal.
- Deliver low-latency question answering through semantic response caching.
- Enable asynchronous document ingestion using an event-driven architecture.
- Generate citation-grounded responses with deterministic validation.
- Evaluate retrieval quality using automated LLM benchmarks.
- Benchmark latency and throughput under concurrent workloads.

### Core Features

- Hybrid GraphRAG retrieval
- Knowledge graph traversal with Neo4j
- Semantic vector search using Qdrant
- Redis-backed semantic response cache
- LangGraph orchestration pipeline
- Apache Kafka event-driven processing
- Automated document ingestion
- Golden Dataset evaluation pipeline
- Citation validation guardrails
- Performance benchmarking with k6

---

# Application User Interface

<p align="center">

UI screenshots will be added soon.

</p>

---

# Demo Video

Demo video will be added.

---

# Tech Stack

| Layer | Technologies | Purpose |
|------|-------------|---------|
| API Layer | FastAPI | High-performance asynchronous API gateway |
| Workflow Orchestration | LangGraph | Stateful GraphRAG execution pipeline |
| LLM | Google Gemini 2.5 Flash | Response generation and evaluation |
| Vector Database | Qdrant | Semantic document retrieval |
| Graph Database | Neo4j | Entity relationship traversal |
| Embeddings | Sentence Transformers | Dense embedding generation |
| Streaming | Apache Kafka | Event-driven ingestion and evaluation |
| Cache | Redis | Semantic response caching |
| Evaluation | Gemini SDK | Faithfulness and relevance benchmarking |
| Backend Runtime | Python | Core application logic |

---

# System Architecture

> A detailed architecture diagram illustrating document ingestion, graph construction, retrieval orchestration, semantic caching, and evaluation workflow will be added soon.

---

# Retrieval Pipeline

```text
                     User Query
                          │
                          ▼
              Semantic Cache (Redis)
                 │                 │
          Cache Hit          Cache Miss
                 │                 │
                 ▼                 ▼
          Return Response    Generate Embedding
                                   │
                                   ▼
                        Vector Search (Qdrant)
                                   │
                                   ▼
                     Knowledge Graph Traversal
                             (Neo4j)
                                   │
                                   ▼
                     LangGraph Orchestration
                                   │
                 ┌─────────────────┴─────────────────┐
                 ▼                                   ▼
         Context Assembly                  Citation Collection
                 │                                   │
                 └─────────────────┬─────────────────┘
                                   ▼
                    Gemini Response Generation
                                   │
                                   ▼
                     Citation Validation Layer
                                   │
                                   ▼
                         Return Final Response
                                   │
                                   ▼
                     Kafka Evaluation Pipeline
```

---

# Performance Benchmarks

The platform was benchmarked using **k6** under concurrent client load to evaluate latency, throughput, and cache effectiveness.

## Architectural Performance

| Metric | Result |
|--------|--------|
| Cache Hit Latency | **35 ms** |
| Cache Miss Latency | **255 ms** |
| Latency Reduction | **~86%** |
| Concurrent Load | **20 Virtual Users** |
| Throughput | **~7 requests/sec** |
| p95 Latency | **1.25 seconds** |

Benchmarks were collected using **k6** against the FastAPI inference endpoint under a sustained load of **20 Virtual Users (VUs)**, comparing requests served through the Redis semantic cache against full GraphRAG retrieval.

## Reliability

- Exponential Backoff + Retry using **Tenacity**
- Event-driven ingestion with **Apache Kafka**
- Asynchronous evaluation workers
- Citation validation before response delivery

## AI Quality

- Automated Golden Dataset evaluation
- Faithfulness benchmarking
- Relevance benchmarking
- Citation verification against retrieved context

---

# Engineering Decisions

The architecture of Keystone prioritizes retrieval quality, system scalability, deterministic response validation, and low-latency inference while keeping retrieval and evaluation loosely coupled.

| Design Decision | Rationale |
|----------------|----------|
| **Why GraphRAG instead of traditional RAG?** | Combines semantic similarity with explicit entity relationships, improving retrieval for multi-hop and cross-document questions. |
| **Why Neo4j?** | Efficient graph traversal enables contextual expansion beyond nearest-neighbor vector search. |
| **Why Qdrant?** | High-performance Approximate Nearest Neighbor search optimized for dense embeddings. |
| **Why Redis Semantic Cache?** | Eliminates repeated LLM inference for semantically similar queries, significantly reducing response latency. |
| **Why LangGraph?** | Provides deterministic orchestration of retrieval, graph expansion, generation, and validation within a stateful workflow. |
| **Why Apache Kafka?** | Decouples document ingestion and evaluation from user-facing inference, improving responsiveness and scalability. |
| **Why Golden Dataset Evaluation?** | Enables repeatable regression testing for retrieval quality as prompts and retrieval strategies evolve. |
| **Why Citation Validation?** | Verifies generated source references against retrieved context to detect unsupported citations before responses are returned. |
| **Why Event-Driven Processing?** | Keeps expensive background operations asynchronous, preventing ingestion and evaluation from blocking inference requests. |
| **Why FastAPI?** | Provides an asynchronous API layer capable of serving concurrent inference requests with minimal overhead. |

---

# Installation & Running the Project

> ⚙️ Detailed setup instructions, Docker Compose configuration, environment variables, and deployment guide will be added soon.

---

# License

Distributed under the **MIT License**.

See the `LICENSE` file for more information.

---

# Author

**Aryan Jaiswal**

- GitHub: https://github.com/AryanJais1224
- LinkedIn: https://www.linkedin.com/in/aryan-jaiswal-618965256/

---
