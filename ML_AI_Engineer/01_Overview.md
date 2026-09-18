---
title: "AI/ML Project Overview"
document_id: "ML-01"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# AI/ML Project Overview

## 1. Introduction

CARIVIX is an AI-powered intelligence platform designed to process user requests, analyze structured and unstructured information, perform machine-learning-based predictions, retrieve relevant information from documents, and generate meaningful responses through AI services.

The AI/ML domain of CARIVIX has been developed as a combination of traditional machine learning, natural-language processing, document intelligence, Retrieval-Augmented Generation (RAG), vector search, large language model inference, and API-based model integration.

The overall objective of the AI/ML engine is to provide an intelligent processing layer between the CARIVIX application/backend and the underlying data, machine-learning models, documents, and language models.

The AI engine is therefore **not a single model**. It is a collection of interconnected services and pipelines that perform different types of intelligence depending on the user's request.

---

## 2. Initial AI/ML Objective

The initial AI/ML work focused on understanding how artificial intelligence could be integrated into the CARIVIX platform and how different AI technologies could support the required business and analytical workflows.

The initial scope included:

- AI/ML architecture design
- Machine-learning workflow definition
- AI model integration
- Natural-language query processing
- Intent classification
- Prediction workflows
- Comparison workflows
- Trend analysis
- Summarization
- Document intelligence
- Retrieval-Augmented Generation
- Large language model integration
- Vector database / vector-search research
- Embedding-model research
- AI evaluation
- Model inference APIs
- Backend integration
- AI technical documentation

---

## 3. Initial Architecture and Research Phase

The early stage of the project concentrated primarily on research and architecture definition. During this phase, different AI technologies and approaches were investigated to determine how they could fit into the CARIVIX architecture.

The research included:

| Area | Focus |
|---|---|
| Machine Learning | Frameworks and modeling approaches |
| NLP | Natural-language processing technologies |
| Large Language Models | Model selection and capabilities |
| LLM Orchestration | Frameworks for managing LLM workflows |
| Embeddings | Embedding-model research |
| Vector Databases | Storage and search technologies |
| Retrieval | Retrieval mechanisms for RAG |
| Prompt Engineering | Structured prompt design |
| RAG Architectures | Retrieval-augmented generation patterns |
| Local LLM Inference | On-premise model execution |
| Model Serving | Serving trained models through APIs |
| AI Evaluation | Measuring quality and performance |
| Guardrails | Response safety and grounding concepts |
| AI Deployment Lifecycle | From research to production |
| Model Monitoring | Experiment tracking and observability |

The purpose of this phase was **not simply to select popular AI tools**. The objective was to understand the role of each technology and determine where it would fit into the CARIVIX AI architecture.

---

## 4. AI Intelligence Layer

As the architecture developed, the AI functionality was organized into an **AI Intelligence Layer**.

The AI Intelligence Layer acts as the processing layer responsible for converting application requests into intelligent operations.

The overall conceptual structure became:

```text
Application
    ↓
Backend / API
    ↓
AI Query Processing
    ↓
AI/ML Service
    ↓
Prediction | Analytics | RAG | LLM Processing
    ↓
Response
```

This separation allows the AI functionality to remain independent from the user interface while still being accessible through backend APIs. It also allows individual AI components to be modified without requiring the complete CARIVIX application to be redesigned.

---

## 5. AI Query Processing

One of the important areas of the CARIVIX AI work is natural-language query processing. The objective is to allow users to communicate with the system using natural language rather than requiring them to know the internal API structure or database structure.

For example, a user may ask for:

- A prediction
- A comparison
- A trend
- A summary
- Information from a project document

The AI query-processing layer determines what the user is requesting and routes the request to the appropriate processing workflow.

**Documented query categories:**

| Category | Purpose |
|---|---|
| Predict | Request a model-based prediction |
| Compare | Request a comparison between entities or values |
| Trend | Request trend analysis over time |
| Summarize | Request a summary of information |

---

## 6. Intent Classification

An intent-classification approach was investigated and documented for identifying the type of request submitted by the user.

**Documented prototype components:**

| Component | Role |
|---|---|
| Python | Implementation language |
| TF-IDF Vectorization | Converts text into numerical features |
| Logistic Regression | Classification algorithm |
| NLP Preprocessing | Text normalization and preparation |
| FastAPI Integration | API exposure of classification |

TF-IDF converts textual queries into numerical feature representations based on the importance of terms within the query. Logistic Regression is then used as the classification algorithm to determine the likely intent.

The output of this stage can be used by the backend to decide which AI service should process the request. This creates a separation between **understanding the request** and **executing the requested operation**.

---

## 7. Prediction and Analytics Engine

In parallel with generative AI development, CARIVIX includes machine-learning-based prediction and analytics workflows.

**Prediction-oriented workflow:**

```text
Data Collection
    ↓
Data Cleaning
    ↓
Data Preprocessing
    ↓
Feature Engineering
    ↓
Model Training / Model Integration
    ↓
Model Evaluation
    ↓
Model Serialization
    ↓
Model Loading
    ↓
Inference
    ↓
API Response Generation
```

The objective is to make trained machine-learning models available to other components of the CARIVIX platform through structured services.

---

## 8. Model-Service Architecture

The model-service layer was designed to provide a standardized interface between trained machine-learning models and the CARIVIX backend.

The model service is responsible for loading trained model artifacts and executing inference when a valid request is received.

**General lifecycle:**

```text
Client Request
    ↓
Request Validation
    ↓
Input Preprocessing
    ↓
Feature Preparation
    ↓
Model Inference
    ↓
Prediction Result
    ↓
Response Formatting
    ↓
JSON Response
```

This approach prevents the backend from directly managing model internals. Instead, the backend communicates with the model service through defined interfaces.

---

## 9. API-Based ML Integration

FastAPI was selected as an important technology for exposing AI/ML functionality through APIs. The documented API work includes prediction and query-processing routes.

**Documented endpoint examples:**

| Endpoint | Purpose |
|---|---|
| `/process/query` | Process a natural-language query |
| `/predict/batch` | Batch prediction execution |
| `/query/predict` | Prediction-oriented query |
| `/query/compare` | Comparison query |
| `/query/trend` | Trend-analysis query |
| `/query/summarise` | Summarization query |

> **Note:** These endpoint names are part of the documented project work. Their exact current production status should always be verified against the latest repository implementation before being described as deployed production APIs.

---

## 10. RAG Development

A major part of the CARIVIX AI development was the introduction of **Retrieval-Augmented Generation (RAG)**.

RAG was selected to allow the AI system to answer questions using project-specific documents and knowledge rather than depending entirely on the information stored inside an LLM.

**Basic concept:**

1. Documents are loaded
2. The text is extracted
3. The text is divided into smaller chunks
4. The chunks are converted into embeddings
5. The embeddings are stored in a vector index
6. A user's question is also converted into an embedding
7. The vector index searches for relevant chunks
8. The retrieved chunks are passed to the LLM as context
9. The LLM generates an answer based on the retrieved information

---

## 11. Document Intelligence

The document-intelligence component is responsible for transforming project documents into searchable knowledge. This process is important because large documents cannot simply be passed directly to an LLM for every request. Instead, documents are processed into smaller units.

**Documented RAG configuration:**

| Parameter | Value |
|---|---|
| Splitter | RecursiveCharacterTextSplitter |
| Chunk Size | ~500 characters |
| Chunk Overlap | ~50 characters |

> The values should be interpreted as **characters** rather than tokens unless the implementation is changed to a token-based splitter.

Chunking allows large documents to be converted into manageable pieces while maintaining some contextual continuity through overlap.

---

## 12. Embedding Generation

After documents are divided into chunks, each chunk is converted into a numerical vector.

**Documented embedding configuration:**

| Parameter | Value |
|---|---|
| Model | SentenceTransformers all-MiniLM-L6-v2 |
| Embedding Dimension | 384 |

The embedding process converts text into numerical representations that can be compared mathematically. The **same embedding model** must be used for document chunks and user queries so that both representations exist in the same vector space.

---

## 13. FAISS Vector Search

FAISS is used as the vector-search component of the documented RAG implementation. The vector index stores embeddings and performs similarity/distance-based searches.

**Documented configuration:**

| Parameter | Value |
|---|---|
| Vector Index | FAISS (L2-based) |
| Default Retrieval | k = 5 |

When a user submits a query, the query is converted into an embedding and searched against the stored document vectors. The system then returns the top relevant chunks.

---

## 14. Local LLM Inference

The CARIVIX RAG implementation uses **Ollama** for local LLM inference.

**Documented model:** Llama 3.1

The reason for using a local inference approach is to provide a development/testing path where the model can run locally rather than requiring every request to be sent to a hosted external LLM service. The LLM receives the user's question together with the retrieved document context and generates the final natural-language response.

---

## 15. RAG Implementation Entry Point

**Documented repository:** `CARIVIX_AI_Model_Training`

**Main execution entry point:** `main_rag.py`

**Documented execution options:**

| Option | Purpose |
|---|---|
| `--index` | Prepare the searchable document representation |
| `--test` | Validate the RAG workflow |
| `--query` | Perform retrieval and response processing |
| `--interactive` | Support repeated user queries |
| `--info` | Provide implementation/configuration information |

---

## 16. AI/RAG Pipeline

The overall documented RAG lifecycle is:

```text
Document Source
    ↓
Document Loading
    ↓
Text Extraction
    ↓
Text Chunking
    ↓
Embedding Generation
    ↓
FAISS Indexing
    ↓
User Query
    ↓
Query Embedding
    ↓
Vector Search
    ↓
Top-K Retrieval
    ↓
Context Construction
    ↓
Prompt Generation
    ↓
Ollama / Llama 3.1 Inference
    ↓
Grounded Response
```

---

## 17. Grounding Requirement

One of the important objectives of the RAG implementation is **grounded response generation**.

A grounded response means that important factual statements in the response should be supported by the retrieved context. The LLM should **not** invent project-specific information when the required information is not available in the retrieved documents.

If the available context does not contain enough information, the expected behavior should be to clearly indicate that the evidence is insufficient rather than generating unsupported information.

---

## 18. Prompt Engineering

Prompt templates were introduced as part of the RAG processing workflow. The purpose of the prompt layer is to provide a consistent structure for:

- System instructions
- User question
- Retrieved context
- Output requirements
- Grounding rules

A prompt template creates a predictable interface between the retrieval system and the LLM. This also makes evaluation easier because different prompt versions can be tested systematically.

---

## 19. AI Evaluation

AI evaluation became an important part of the implementation process. Evaluation is required because successful execution of an AI pipeline does not automatically mean that the output is correct.

**CARIVIX AI evaluation scope:**

| Area | Purpose |
|---|---|
| Retrieval Relevance | Was the correct information retrieved? |
| Response Relevance | Does the response address the query? |
| Factuality | Is the response factually correct? |
| Groundedness | Is the response supported by retrieved context? |
| Response Quality | Is the response clear and complete? |
| Latency | How fast is the pipeline? |
| Failure Analysis | What went wrong and where? |

The evaluation process separates **retrieval quality** from **generation quality**:

- If the correct document was **not** retrieved → primarily a **retrieval** problem
- If the correct document **was** retrieved but the LLM generated an unsupported answer → primarily a **generation / prompt / grounding** problem

---

## 20. Latency Evaluation

Latency is another important engineering metric. The total response time can be separated into:

```text
Query Embedding Time
    +
Vector-Search Time
    +
Context-Construction Time
    +
LLM Generation Time
    =
Total API Response Time
```

Separating these measurements helps identify which component is responsible for performance problems.

---

## 21. Sprint 3 Development

Sprint 3 focused on moving the AI architecture toward implementation and integration.

**Major AI/ML work:**

- AI architecture integration planning
- Backend/API alignment
- AI stack finalization
- Development-environment validation
- RAG architecture implementation planning
- Ollama local inference
- Embedding-model integration
- FAISS vector-search integration
- Model inference requirements
- AI pipeline organization

The objective of this stage was to establish the technical foundation required for the next implementation stage.

---

## 22. Sprint 4 Development

Sprint 4 moved further into implementation validation and engineering refinement.

**Documented Sprint 4 implementation areas:**

- Identifying pipeline failures
- Improving document ingestion
- Implementing and validating the document chunking strategy
- Validating metadata handling
- Improving the embedding pipeline
- Improving the retrieval pipeline
- Testing vector search
- Comparing retrieval results
- Connecting retrieved context to LLM processing
- Implementing prompt templates
- Testing grounded responses
- Creating an AI evaluation test set
- Testing relevance
- Testing factuality
- Measuring latency
- Documenting architecture and implementation results

---

## 23. Current AI Implementation Review

The latest work has focused on reviewing the AI implementation plan against the existing CARIVIX AI/RAG architecture.

**Review scope:**

- Checking whether the proposed AI workflow matches the existing architecture
- Reviewing the model-service architecture
- Reviewing the relationship between model services and the RAG pipeline
- Checking indexing and retrieval behavior
- Identifying AI/ML integration gaps
- Identifying areas that require implementation changes or further validation
- Coordinating technical updates with the technical-writing process

---

## 24. Current RAG Validation

The latest implementation review included execution of the RAG workflow through `main_rag.py`. The indexing and retrieval process was tested.

A test query produced a relevant top retrieval with a reported score around **0.72**.

> **Important:** This value must **not** automatically be interpreted as 72% accuracy. Because the documented FAISS configuration uses **L2 distance**, the numerical value represents the configured retrieval distance/score behavior and requires a defined evaluation methodology before it can be converted into an accuracy or percentage claim.

---

## 25. Current Technical Stack

| Component | Technology |
|---|---|
| Language | Python 3.11 |
| API Framework | FastAPI |
| AI/RAG Framework | LangChain |
| Text Splitter | RecursiveCharacterTextSplitter |
| Embedding Framework | SentenceTransformers |
| Embedding Model | all-MiniLM-L6-v2 |
| Vector Index | FAISS |
| LLM Runtime | Ollama |
| Primary LLM | Llama 3.1 |
| Classical ML | Scikit-learn |
| Feature Representation | TF-IDF |
| Classifier | Logistic Regression |
| Experiment Tracking | MLflow (SQLite) |
| Data Manipulation | Pandas, NumPy |

> The exact version of each dependency should be taken from the current project environment or dependency file when producing a final release document.

---

## 26. Data and Knowledge Sources

**Documented datasets:**

| Dataset | Type |
|---|---|
| Market Analysis 1981–2025.csv | Analytical |
| arxiv.csv | Research / Document |
| Economic Trend Analysis.csv | Analytical |
| Public Program Evaluation.csv | Analytical |
| Traffic Analysis.csv | Analytical |

These datasets support analytical / model-oriented workflows. Document sources support the RAG / document-intelligence workflow.

**The two data paths should remain conceptually separate:**

```text
Structured Analytical Data → ML / Analytics Pipeline
Unstructured Documents      → RAG Pipeline
```

---

## 27. MLflow and Experiment Tracking

The repository documentation references **MLflow** with SQLite configuration. MLflow can support experiment and model lifecycle tracking.

**A complete tracking process should capture:**

- Model version
- Dataset version
- Features
- Hyperparameters
- Evaluation metrics
- Training environment
- Artifact location
- Execution date

This provides reproducibility and makes it easier to compare different model versions.

---

## 28. Architectural Separation

The current AI architecture is organized around several distinct responsibilities:

| Layer | Responsibility |
|---|---|
| Query Processing | Determines what the user is requesting |
| Prediction Services | Execute trained models |
| RAG | Retrieves relevant document information |
| Embedding Layer | Converts text into vectors |
| FAISS | Performs vector search |
| Prompt Layer | Prepares the LLM input |
| LLM | Generates natural-language responses |
| Evaluation Layer | Measures quality and performance |
| API Layer | Connects services to the rest of CARIVIX |

---

## 29. Implementation vs Conceptual Design

A major documentation requirement is to **distinguish between implemented functionality and architectural concepts**.

A component should be described as **implemented** only when supported by code, configuration, or execution evidence. A component should be described as **planned or conceptual** when it exists only in architecture documentation or future implementation plans.

This distinction is especially important for:

- AI agents
- Advanced guardrails
- Production monitoring
- Automatic evaluation
- Advanced model routing
- External LLM providers
- Production-scale vector databases
- Automated model retraining

These should not be presented as implemented unless current repository evidence confirms them.

---

## 30. Current Engineering Direction

The current direction of the CARIVIX AI/ML engine is toward a more integrated and testable AI system.

**Major engineering priorities:**

- Strengthening document ingestion
- Validating chunking
- Improving metadata preservation
- Improving embedding and retrieval quality
- Testing vector-search behavior
- Improving retrieved-context handling
- Standardizing prompt templates
- Improving grounded responses
- Building an evaluation dataset
- Measuring relevance and factuality
- Measuring latency
- Strengthening model-service integration
- Resolving backend integration gaps
- Maintaining accurate technical documentation

---

## 31. Overall Project Evolution

The CARIVIX AI/ML work has progressed through several broad stages:

| Stage | Focus |
|---|---|
| Stage 1 | AI scope identification and research |
| Stage 2 | AI architecture and technology-stack definition |
| Stage 3 | Model-service and query-processing design |
| Stage 4 | RAG architecture and implementation |
| Stage 5 | Embedding and vector-search integration |
| Stage 6 | Local LLM inference through Ollama |
| Stage 7 | Prompt and grounded-response implementation |
| Stage 8 | AI evaluation and latency testing |
| Stage 9 | Sprint-based implementation refinement |
| Stage 10 | Current architecture review, integration-gap analysis, and technical documentation |

---

## 32. Current State of the CARIVIX AI/ML Engine

The current AI/ML engine should be understood as a **multi-component intelligence layer** rather than a single AI model.

**Major capabilities and engineering components:**

- Natural-language query processing
- Intent classification
- Prediction and analytics workflows
- Machine-learning model inference
- FastAPI model services
- Document ingestion
- Document chunking
- Text embeddings
- FAISS vector retrieval
- RAG context construction
- Prompt templates
- Local LLM inference
- Grounded response generation
- AI evaluation
- Latency measurement
- Backend / API integration
- Technical architecture documentation

---

## 33. Final Project Position

The CARIVIX AI/ML implementation has progressed from initial AI research and architecture planning toward implementation-oriented AI services. The current technical foundation combines conventional machine-learning inference with modern retrieval-based generative AI.

| Layer | Role |
|---|---|
| Prediction Path | Provides model-driven analytical intelligence |
| RAG Path | Provides document-grounded generative intelligence |
| Query-Processing Layer | Routes natural-language requests to the appropriate AI capability |
| API Layer | Integrates the AI engine with the wider CARIVIX platform |
| Evaluation Layer | Measures retrieval quality, factual support, and performance |

The next level of maturity depends on continued repository-level validation, integration testing, measurable evaluation results, model/version tracking, and clear separation between implemented capabilities and planned architecture.

This overview therefore represents the complete technical progression of the CARIVIX AI/ML domain from its initial architecture and research phase through the current implementation, validation, integration-review, and documentation stage.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — AI/ML project overview |
