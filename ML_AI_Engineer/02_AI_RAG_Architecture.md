---
title: "AI/RAG Architecture"
document_id: "ML-02"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# AI/RAG Architecture

## 1. Architecture Overview

The CARIVIX AI/RAG architecture is designed as an intelligent processing layer that connects the CARIVIX application and backend services with machine-learning models, document knowledge, vector retrieval, and large language model inference.

The architecture combines **two major intelligence paths**:

| Path | Responsibility |
|---|---|
| **Machine Learning / Prediction Engine** | Executes trained machine-learning models and returns structured analytical or predictive results |
| **Retrieval-Augmented Generation (RAG) Engine** | Processes project documents, creates searchable vector representations, retrieves relevant information for a user query, and provides that information as context to an LLM before generating a response |

### General Architectural Principle

```text
User / Application Request
    ↓
Backend / API Layer
    ↓
AI Processing Layer
    ├──────────────────────┐
    ↓                      ↓
Prediction Engine      RAG Engine
    ↓                      ↓
ML Models          Document Knowledge
                           ↓
                    Vector Retrieval
                           ↓
                     LLM Inference
    └──────────┬───────────┘
               ↓
          AI Response
```

The architecture is intentionally separated into logical components so that document retrieval, machine-learning inference, language-model processing, and API integration can evolve independently.

---

## 2. High-Level CARIVIX AI Architecture

The high-level architecture represents the complete interaction between the application, backend, AI services, prediction services, document/RAG services, and response layer.

### Architectural Layers

| Layer | Responsibility |
|---|---|
| **Application Layer** | Provides the user-facing interface and submits requests |
| **Backend / API Layer** | Receives requests and communicates with AI services |
| **AI Query Processing Layer** | Determines the intended operation and routes the request |
| **Prediction Engine** | Executes machine-learning models |
| **RAG Engine** | Retrieves relevant information from project documents |
| **Embedding Layer** | Converts text into numerical vector representations |
| **Vector Search Layer** | Searches the FAISS index for relevant content |
| **LLM Layer** | Uses retrieved context to generate a natural-language response |
| **Response Layer** | Formats the result and returns it to the application |

---

## 3. Core RAG Architecture

The RAG architecture is divided into **two primary pipelines**:

| Pipeline | Purpose |
|---|---|
| **A. Offline / Indexing Pipeline** | Prepares the knowledge base before users submit queries |
| **B. Online / Query Pipeline** | Processes a user's question at runtime |

This separation is important because document processing and embedding generation do not need to be repeated for every user query.

**Key principle:** The indexing pipeline creates the searchable knowledge representation. The query pipeline uses that representation to retrieve relevant information. The two pipelines **meet at the vector-search layer**.

---

## 4. Document Ingestion and Chunking

The first major RAG component is **document ingestion**. Its purpose is to transform source documents into machine-processable text.

### General Process

```text
Source Document
    ↓
Document Loader
    ↓
Text Extraction
    ↓
Document Object
    ↓
Chunking
    ↓
Searchable Document Chunks
```

### Documented Configuration

| Parameter | Value |
|---|---|
| Framework | LangChain-based document processing |
| Splitter | RecursiveCharacterTextSplitter |
| Chunk Size | ~500 characters |
| Chunk Overlap | ~50 characters |

> These values should be treated as **character-based** configuration unless the current implementation is changed to use a token-based splitter.

### Chunk Overlap Example

| Chunk | Character Range |
|---|---|
| Chunk 1 | Characters 1–500 |
| Chunk 2 | Characters 451–950 |
| Chunk 3 | Characters 901–1400 |

The overlap helps reduce the possibility of losing contextual information when a sentence or concept crosses a chunk boundary.

### Chunking Quality Considerations

Chunking quality directly affects retrieval quality:

- **Chunks too large** → irrelevant information may be retrieved along with the required information
- **Chunks too small** → important context may be separated across multiple chunks

Therefore, chunk size and overlap should be treated as **retrieval-quality parameters** rather than arbitrary constants.

---

## 5. Embedding and Vector Search Architecture

After document chunks are generated, each chunk is converted into a numerical embedding.

### Documented Embedding Configuration

| Parameter | Value |
|---|---|
| Embedding Model | SentenceTransformers |
| Model | all-MiniLM-L6-v2 |
| Vector Dimension | 384 |

### Conceptual Flow

```text
Text Chunk
    ↓
Embedding Model
    ↓
384-Dimensional Vector
```

> The **same embedding model** should be used when converting user queries into vectors. This is necessary because document embeddings and query embeddings must exist in a **compatible vector space** for meaningful retrieval.

### Vector Search

| Parameter | Value |
|---|---|
| Vector Index | FAISS |
| Index Type | L2-based |
| Default Retrieval | Top-K = 5 |

The retrieval layer is configured to return up to **five relevant chunks** for downstream context construction.

> **Important:** The retrieval score must be interpreted according to the configured distance/search mechanism. A numerical retrieval score must **not** automatically be described as an accuracy percentage.

---

## 6. RAG Query Processing and LLM Integration

At runtime, a user submits a natural-language question. The query follows a sequence of processing stages.

### Query Processing Flow

```text
User Query
    ↓
Query Embedding
    ↓
FAISS Search
    ↓
Top-K Retrieved Chunks
    ↓
Context Construction
    ↓
Prompt Template
    ↓
Ollama
    ↓
Llama 3.1
    ↓
Generated Response
```

The LLM does not need to independently know all project-specific information. Instead, the **retrieved context is supplied as part of the prompt**. This is the main architectural distinction between ordinary LLM generation and RAG-based generation.

---

## 7. Prompt, Grounding and Response Architecture

The prompt layer connects retrieved evidence with LLM generation.

### General RAG Prompt Structure

```text
System Instructions
    +
Retrieved Context
    +
User Question
    +
Response Requirements
```

### Grounded Response Requirements

A grounded response should:

- Use information contained in the retrieved context
- Avoid unsupported project-specific claims
- Avoid inventing missing information
- Distinguish between available evidence and unsupported assumptions
- Indicate when sufficient context is not available

### Architectural Dependency

The RAG architecture depends on **both retrieval quality and generation behavior**:

- Even a strong LLM can produce an incorrect answer if the retrieval layer supplies irrelevant information
- Correct retrieved context can still produce a poor response if the prompt does not properly constrain the LLM

---

## 8. CARIVIX RAG Implementation Structure

The documented CARIVIX AI model-training repository contains the RAG implementation components required for indexing and querying.

**Main execution entry point:** `main_rag.py`

### Documented Command-Line Operations

| Option | Purpose |
|---|---|
| `--index` | Document indexing and vector-store preparation |
| `--test` | Testing the RAG implementation |
| `--query` | Execute a query against the RAG system |
| `--interactive` | Interactive query processing |
| `--info` | Display implementation / configuration information |

The repository therefore provides an execution path for **both preparation and runtime querying**. The indexing process should normally be completed whenever the underlying document knowledge base changes significantly.

---

## 9. Technology Selection and Technical Fit

The major technologies used in the documented architecture have different responsibilities.

| Technology | Architectural Responsibility |
|---|---|
| **Python 3.11** | Primary implementation language for AI/ML components — supports ML, NLP, document processing, embeddings, vector search, API services, and LLM integration |
| **FastAPI** | API layer for exposing AI/ML functionality with structured request/response handling |
| **LangChain** | Document loading, text splitting, and orchestration of retrieval-related components |
| **RecursiveCharacterTextSplitter** | Divides documents into smaller character-based chunks with overlap |
| **SentenceTransformers** | Embedding-generation functionality |
| **all-MiniLM-L6-v2** | Embedding model for converting text into 384-dimensional vectors |
| **FAISS** | Vector indexing and search for similarity/distance-based retrieval |
| **Ollama** | Local LLM execution and model serving |
| **Llama 3.1** | Documented LLM used for local RAG response generation |
| **MLflow** | Experiment / model lifecycle tracking |
| **SQLite** | Documented MLflow configuration store |

Each technology therefore has a **defined architectural responsibility** rather than being included only as a general-purpose dependency.

---

## 10. AI/RAG and Model-Service Integration

The RAG engine and prediction engine are **separate processing paths** but belong to the same **AI Intelligence Layer**.

| Engine | Responsibility |
|---|---|
| **Model-Service Architecture** | Trained-model inference |
| **RAG Architecture** | Document-grounded language generation |

They can be integrated at the **query-routing layer**.

### Query Routing Principle

This separation is important because **not every user question should be sent to an LLM**:

- A **numerical prediction** should normally be processed by the appropriate trained model
- A **question asking for information from project documentation** can be processed through RAG
- A **trend or comparison request** may require structured analytical processing

The query-processing layer therefore acts as an **architectural routing mechanism**.

---

## 11. Failure Points, Validation and Current Integration Status

### Potential Failure Points

| Failure Point | Description |
|---|---|
| **Document Ingestion Failure** | A document cannot be loaded or text cannot be extracted correctly → knowledge base will be incomplete |
| **Chunking Failure** | Incorrect chunk size, overlap, or document boundaries → reduced retrieval quality |
| **Metadata Failure** | Missing or incorrect metadata → document traceability and filtering become difficult |
| **Embedding Failure** | Embeddings not generated correctly → corresponding chunks cannot participate in vector search |
| **Vector-Index Failure** | Corrupted or incorrectly built FAISS index → invalid retrieval behavior |
| **Retrieval Failure** | Query may retrieve irrelevant or incomplete chunks |
| **Prompt-Construction Failure** | Retrieved context may not be inserted correctly into the LLM prompt |
| **LLM Inference Failure** | Ollama or the selected model may not be available or may fail during inference |
| **Grounding Failure** | The LLM may produce information that is not supported by the retrieved context |
| **API Integration Failure** | AI response may not be correctly passed back to the backend/application |

### Current Validation Status

Current engineering work has focused on identifying and addressing these integration points. The RAG workflow has been executed through the documented `main_rag.py` entry point for indexing and query validation.

A test retrieval produced a top result with a reported score around **0.72**.

> This should be interpreted as a **retrieval score / distance result** rather than an accuracy percentage. A formal retrieval-quality metric requires a defined evaluation dataset and evaluation methodology.

---

## 12. Architectural Boundaries and Current Limitations

The current architecture provides the foundation for document-grounded AI processing, but several areas require continued engineering and validation.

### Capability Classification

The architecture should maintain a clear distinction between:

- **Implemented** components
- **Validated** components
- **Documented** components
- **Planned** components
- **Potential future** components

### Areas Not to Be Represented as Fully Implemented

The following areas should not be represented as fully implemented unless current code evidence confirms them:

- Production-grade automated guardrails
- Enterprise-scale vector databases
- Automatic model retraining
- Fully automated evaluation pipelines
- Advanced agentic orchestration
- Production monitoring
- Automatic model routing
- External LLM failover
- Large-scale distributed inference

The documented architecture currently provides the foundation for these capabilities but does **not** mean that every future capability is already implemented.

### Document Quality Dependency

RAG quality depends strongly on the quality of the underlying documents. If the source document is incorrect, incomplete, outdated, or poorly structured, retrieval and generation quality can also be affected.

### Retrieval Quality Factors

Retrieval quality depends on:

- Chunk size
- Chunk overlap
- Embedding-model quality
- Vector-index configuration
- Query quality
- Top-K selection
- Document coverage
- Metadata quality
- Prompt design

Therefore, **RAG performance should be measured experimentally** instead of being inferred solely from successful execution.

---

## 13. Current Architecture Status and Conclusion

The CARIVIX AI/RAG architecture has progressed from an initial AI research and architecture-definition stage into an **implementation-oriented AI processing architecture**.

### Architectural Separation

The current architecture establishes a separation between:

- AI query processing
- Machine-learning inference
- Document ingestion
- Document chunking
- Embedding generation
- Vector retrieval
- Context construction
- Prompt processing
- LLM inference
- Grounded response generation
- API integration
- AI evaluation

### Documented RAG Pipeline

```text
Documents
    → Document Loading
    → Text Extraction
    → Recursive Character Chunking
    → Embedding Generation
    → 384-Dimensional Vectors
    → FAISS L2 Index
    → User Query
    → Query Embedding
    → Top-K Retrieval
    → Context Construction
    → Prompt Template
    → Ollama
    → Llama 3.1
    → Grounded Response
```

### Separate Prediction Path

```text
User Request
    → Query Processing
    → Model Service
    → Trained ML Model
    → Inference
    → Structured Result
```

These two paths can be connected through the **AI query-processing layer**, allowing CARIVIX to select an appropriate intelligence workflow according to the type of request.

### Current Technical Foundation

| Component | Technology |
|---|---|
| Language | Python 3.11 |
| API Framework | FastAPI |
| RAG Framework | LangChain |
| Text Splitter | RecursiveCharacterTextSplitter |
| Embedding Framework | SentenceTransformers |
| Embedding Model | all-MiniLM-L6-v2 |
| Vector Index | FAISS |
| LLM Runtime | Ollama |
| Primary LLM | Llama 3.1 |
| Experiment Tracking | MLflow |

### Next Engineering Focus

The next engineering focus is to strengthen the reliability of the complete pipeline by validating:

- Document ingestion
- Chunking
- Metadata
- Embedding generation
- Retrieval relevance
- Context construction
- Prompt behavior
- Grounded responses
- Latency
- Backend integration

### Most Important Architectural Principle

> The RAG system should **not** be evaluated only by whether it produces a response. It should be evaluated based on whether it:
> - Retrieves relevant evidence
> - Uses that evidence correctly
> - Generates factually supported responses
> - Provides acceptable response latency

### Final Architectural Objective

```text
Reliable Data
    +
Reliable Retrieval
    +
Controlled Context
    +
Appropriate AI/ML Processing
    +
Grounded Generation
    +
Validated API Integration
    =
CARIVIX AI Intelligence
```

Overall, the CARIVIX AI/RAG architecture provides the technical foundation for combining structured machine-learning intelligence with document-grounded generative AI. The architecture is **modular**, allowing individual components such as embedding models, vector indexes, LLMs, prompt templates, or model services to be improved independently while maintaining the overall **AI Intelligence Layer**.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Nerella Raghavendra Guptha | Initial version — AI/RAG architecture |
