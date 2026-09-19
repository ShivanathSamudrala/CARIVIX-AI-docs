---
title: "CARIVIX AI — API & Module Integration"
document_id: "API-07"
version: "1.0"
status: "Final"
last_updated: "2026-09-19"
author: "Shivanath Samudrala"
role: "Technical Writer"
---

# CARIVIX AI — API & Module Integration

## 1. Purpose

This document describes the **technical integration of the CARIVIX AI platform** at the API, module, ML inference, NLP routing, RAG, vector-search, and response-generation levels.

It has been updated with the **Sprint 5 API Testing & Postman Validation results**, which provide implementation-level evidence that the major API components are operational.

### Documentation Coverage

| # | Area |
|---|---|
| 1 | API architecture |
| 2 | FastAPI integration |
| 3 | API endpoints |
| 4 | Module responsibilities |
| 5 | NLP and intent routing |
| 6 | ML model integration |
| 7 | RAG integration |
| 8 | FAISS vector retrieval |
| 9 | LLM integration |
| 10 | Combined AI routing |
| 11 | Validation and error handling |
| 12 | Postman testing |
| 13 | Automated regression testing |

---

## 2. Primary Integration Objective

The primary objective is to provide a **single integration layer** through which CARIVIX AI can expose ML prediction and AI/RAG functionality through REST APIs.

### High-Level Architecture

```text
CARIVIX AI
    ↓
FastAPI API Layer
    ↓
Request Validation
    ↓
NLP / AI Routing
    ↓
┌───────┼───────┐
↓       ↓       ↓
RAG     ML      Combined
↓       ↓       ↓
FAISS + LLM / ML Models / RAG + ML
    ↓
JSON API Response
```

---

## 3. Overall CARIVIX AI Architecture

CARIVIX AI is structured around **two major processing engines**:

| # | Engine |
|---|---|
| 1 | AI/RAG Engine |
| 2 | Prediction/ML Engine |

> The API layer provides the **integration boundary** between external clients and these engines.

### 3.1 Overall Architecture

```text
Client / Postman / Frontend
            ↓
    FastAPI API Layer
            ↓
    Request Validation
            ↓
    AI / NLP Routing
            ↓
   ┌────────┴─────────┐
   ↓                  ↓
AI / RAG Engine    Prediction Engine
   ↓                  ↓
RAG Pipeline       ML Model Service
   ↓                  ↓
Documents          Preprocessing
   ↓                  ↓
Chunking           Feature Engineering
   ↓                  ↓
Embedding Model    (returns to API Response)
   ↓
FAISS Vector Store
   ↓
Retriever
   ↓
Prompt Builder
   ↓
LLM
   ↓
API Response
```

### 3.2 Integration Philosophy

The architecture **separates responsibilities** instead of placing API, model processing, retrieval, and generation into one component.

**This provides:**

| # | Benefit |
|---|---|
| 1 | Modular development |
| 2 | Independent testing |
| 3 | Easier debugging |
| 4 | Model replacement capability |
| 5 | Independent RAG testing |
| 6 | API-level validation |
| 7 | Easier future deployment |

---

## 4. Repository and Module Structure

The CARIVIX AI repository contains the implementation required for API serving, ML processing, RAG processing, evaluation, and testing.

### Important Integration Modules

```text
CARIVIX_AI_Model_Training/
├── api.py                    ← FastAPI application
├── ai_integration.py         ← AI/RAG + ML integration layer
├── nlp_module.py             ← NLP intent routing
├── train_intent_classifier.py ← Intent classifier training
├── main.py                   ← ML training pipeline
├── main_rag.py               ← RAG pipeline CLI
├── run_baseline_pipeline.py  ← Baseline model comparison
├── evaluate_rag.py           ← RAG evaluation
├── evaluate_test_set.py      ← Test set evaluation
├── data_validation.py        ← Data validation
├── database_service.py       ← Database service
├── config/
│   └── config.yaml
├── data/
│   ├── raw/
│   ├── processed/
│   └── documents/
└── models/
```

---

## 5. FastAPI Application and API Integration

### 5.1 API Layer

The FastAPI application is the **primary runtime interface** for CARIVIX AI.

**The server provides access to:**

| # | Capability |
|---|---|
| 1 | Health information |
| 2 | Model information |
| 3 | Model discovery |
| 4 | ML inference |
| 5 | Batch inference |
| 6 | AI/RAG queries |
| 7 | OpenAPI documentation |

**Tested Environment:**

| Parameter | Value |
|---|---|
| Operating System | Windows |
| Python | 3.14.6 |
| Environment | Project venv |
| API | FastAPI / Uvicorn |
| Base URL | `http://127.0.0.1:8000` |

### 5.2 API Architecture

System architecture diagram — see overall architecture in 
[System_Architecture](https://github.com/ShivanathSamudrala/CARIVIX-AI-docs/blob/main/Knowledge%20Base%20/03_System_Design/08.%20System_Architecture.md)

### 5.3 Why FastAPI is Used

| # | Capability |
|---|---|
| 1 | REST API support |
| 2 | Automatic validation |
| 3 | Automatic OpenAPI generation |
| 4 | Swagger documentation |
| 5 | Structured HTTP errors |
| 6 | Asynchronous / server compatibility |
| 7 | Python integration with ML services |

---

## 6. API Endpoints and Integration Contracts

### 6.1 Health Endpoint

**Endpoint:** `GET /health`

**Purpose:**

| # | Purpose |
|---|---|
| 1 | Verify service availability |
| 2 | Check model loading |
| 3 | Identify model failures |

**Validated Result:**

```json
{
  "status": "healthy",
  "models_loaded": 8,
  "models_failed": 0
}
```

**Latency:** 8.9 ms

This confirms that the API process was active and all eight configured models were available to the serving layer.

### 6.2 Model Listing

**Endpoint:** `GET /api/v1/models`

**Purpose:** Return the models available to the inference service.

**Sprint 5 Result:**

| Metric | Value |
|---|---|
| HTTP Status | 200 |
| Result | PASS  |
| Models Returned | 8 |

### 6.3 Model Information

**Endpoint:** `GET /api/v1/model/info`

**Purpose:** Return information about the configured/default prediction model.

**Result:**

| Metric | Value |
|---|---|
| HTTP Status | 200 |
| Result | PASS  |
| Latency | 27.5 ms |

### 6.4 Single Prediction

**Endpoint:** `POST /api/v1/predict`

This endpoint accepts structured applicant/model features.

**Tested Feature Set:**

| # | Feature |
|---|---|
| 1 | `age` |
| 2 | `income` |
| 3 | `credit_score` |
| 4 | `loan_amount` |
| 5 | `years_employed` |
| 6 | `education` |
| 7 | `employment_status` |
| 8 | `marital_status` |
| 9 | `housing_type` |
| 10 | `application_date` |

**Request Processing Flow:**

```text
API
 ↓
Validation
 ↓
Model Service
 ↓
Preprocessing
 ↓
Feature Engineering
 ↓
Selected Model
 ↓
Prediction
```

### 6.5 Batch Prediction

**Endpoint:** `POST /api/v1/predict/batch`

This endpoint allows multiple records to be processed through a single API call.

**Sprint 5 Validation:**

| Metric | Value |
|---|---|
| Records Processed | 2 applicant records |
| HTTP Status | 200 |
| Result | PASS  |
| Latency | 187.6 ms |

### 6.6 AI Query

**Endpoint:** `POST /api/v1/ai/query`

This is the primary natural-language AI integration endpoint.

**Supported Processing Routes:**

```text
Natural Language Query
        ↓
NLP / Intent Analysis
        ↓
Route Selection
        ├─── RAG
        ├─── ML
        └─── Combined
```

---

## 7. NLP, Intent Classification and Query Routing

The NLP layer analyzes a natural-language request before selecting the downstream processing route.

### 7.1 Processing Flow

```text
User Query
    ↓
NLP Analysis
    ├─→ Intent
    ├─→ Confidence
    ├─→ Entities
    └─→ Route
    ↓
AI Integration
```

The system can route a query toward:

| # | Route |
|---|---|
| 1 | RAG |
| 2 | ML |
| 3 | Combined |

### 7.2 RAG Routing

**Example Query:** `"What is CARIVIX AI?"`

**Result:** The system retrieved relevant chunks and generated an answer from the available context.

### 7.3 ML Routing

**Example Query:** `"Predict the customer churn probability for this account"`

**Result:** `Route = ml`

The API correctly identified the ML requirement.

Importantly, the test also verified that the system did **not** falsely claim to have all required structured features. Instead, it reported that automatic feature extraction did not have the complete model field set and requested the required feature set through the prediction API.

This is an important validation of the current integration boundary.

### 7.4 Combined Routing

**Example Query:** `"Explain economic forecasting"`

**Result:** `Route = combined`

The system retrieved relevant context and generated the response.

---

## 8. AI / RAG Engine Integration

The RAG engine follows a multi-stage pipeline.

```text
Documents
    ↓
Document Loader
    ↓
Text Cleaning
    ↓
Chunking
    ↓
Embedding Model
    ↓
FAISS Index
    ↓
Retriever
    ↓
Prompt Builder
    ↓
LLM
    ↓
Grounded Response
```

### 8.1 Document Loading

Documents are loaded into the RAG pipeline. The loader converts source documents into a processable representation.

### 8.2 Chunking

Large documents cannot normally be passed directly to the LLM. Therefore:

```text
Document
    ↓
Smaller chunks
    ↓
Embedding
    ↓
Vector index
```

The evaluation used:

| Parameter | Value |
|---|---|
| Chunk Size | 300 |
| Overlap | 50 |

### 8.3 Embeddings

Each text chunk is converted into a numerical vector.

```text
Text Chunk
    ↓
Embedding Model
    ↓
Vector
```

These vectors allow semantic similarity comparisons.

### 8.4 FAISS

FAISS provides vector similarity search.

The query follows:

```text
Question
    ↓
Query Embedding
    ↓
FAISS Search
    ↓
Top-K Similar Chunks
```

**Postman RAG Test:**

For the CARIVIX query `"What is CARIVIX AI?"` the system retrieved:

| Metric | Value |
|---|---|
| Relevant chunks | 3 |
| Similarity | 0.7521 |

### 8.5 Prompt Construction

The retrieved chunks are inserted into the prompt context.

```text
User Question
      +
Retrieved Context
      ↓
Final Prompt
```

### 8.6 Response Generation

The LLM generates a response using the retrieved context.

This is the key distinction between ordinary text generation and the CARIVIX RAG path:

```text
Query
  ↓
Evidence Retrieval
  ↓
Context
  ↓
Generation
```

---

## 9. Prediction Engine and ML Model Integration

The Prediction Engine provides structured ML inference.

### 9.1 Prediction Architecture

*(See [Section 3.1](#31-overall-architecture) for the architecture diagram)*

### 9.2 Models Validated

The health/model testing confirmed that all eight models were loaded:

| # | Model |
|---|---|
| 1 | LogisticRegression |
| 2 | NaiveBayes |
| 3 | DecisionTree |
| 4 | GradientBoosting |
| 5 | XGBoost |
| 6 | SVM |
| 7 | KNN |
| 8 | RandomForest |

**Health Result:**

```json
{
  "models_loaded": 8
}
```

**8/8 models loaded** 
### 9.3 Logistic Regression Validation

The default `LogisticRegression` model returned:

| Metric | Value |
|---|---|
| Prediction | 1 |
| Confidence | 0.6485 |
| Probability | 0.6485 |
| Latency | 239.5 ms |

This validates the complete API-to-model inference path.

### 9.4 RandomForest Validation

A targeted `RandomForest` request returned:

| Metric | Value |
|---|---|
| Prediction | 1 |
| Confidence | 0.520 |
| Latency | 206.6 ms |

This confirms that the API can target a specific loaded model rather than being limited to a single model implementation.

---

## 10. Natural Language → ML Integration

Natural-language ML requests require special handling because the prediction model expects structured features.

**Example Query:** `"Predict the customer churn probability for this account"`

This query does not necessarily contain:

- `age`
- `income`
- `credit_score`
- `loan_amount`
- …

Therefore, the validated architecture is:

```text
Natural Language
        ↓
NLP / Intent Detection
        ↓
ML Route
        ↓
Check Required Features
        ├─── Complete ──→ Prediction
        └─── Missing ───→ Request Feature Set
```

The system correctly selected the ML route but **did not fabricate missing fields**.

This is an important quality-control mechanism because automatically inventing model features could produce misleading predictions.

---

## 11. Combined RAG + ML Integration

The combined route is intended for queries requiring contextual information **and** analytical/model processing.

### Architecture

```text
Natural Language Query
          ↓
NLP / Intent Analysis
          ↓
Combined Route
   ├──────────────────┐
   ↓                  ↓
RAG Retrieval     ML Processing
   ↓                  ↓
Retrieved Context  Structured Features
   ↓                  ↓
LLM                Prediction
   └────────┬─────────┘
            ↓
    Combined Response
```

**Test Query:** `"Explain economic forecasting"`

| Metric | Value |
|---|---|
| Route | combined |
| Result | PASS  |
| Latency | 7.17 seconds |

The system successfully retrieved relevant context and generated the response.

>  The combined route should still be considered an integration area requiring further refinement for complete automatic ML feature mapping.

---

## 12. End-to-End API Data Flow

The complete CARIVIX AI runtime can be represented as:

```text
Client Request
      ↓
FastAPI API Layer
      ↓
Request Validation
      ↓
NLP / AI Routing
      ↓
┌─────────────┼─────────────┐
↓             ↓             ↓
RAG Path      ML Path       Combined Path
↓             ↓             ↓
FAISS + LLM   ML Models     RAG + ML
└─────────────┼─────────────┘
              ↓
      JSON API Response
```

---

## 13. Error Handling, Validation and Out-of-Domain Control

API integration is not complete without failure-path validation.

### 13.1 Empty Query Validation

**Test:** `POST /api/v1/ai/query` with an empty query.

| Metric | Value |
|---|---|
| Expected | HTTP 400 |
| Actual | HTTP 400 |
| Response | `"Empty query"` |
| Result | PASS  |

### 13.2 Invalid Prediction Payload

**Test:** `POST /api/v1/predict` with invalid/missing fields.

| Metric | Value |
|---|---|
| Expected | HTTP 422 |
| Actual | HTTP 422 |
| Result | PASS  |

This confirms that request validation prevents invalid data from reaching the model layer.

### 13.3 Out-of-Domain Handling

**Query:** `"What is the capital of France?"`

| Metric | Value |
|---|---|
| Expected | Unsupported information should not be fabricated |
| Actual | `"Information not found."` |
| Result | PASS  |

This validates the system's context-grounding behavior for information unavailable in the indexed knowledge.

---

## 14. Postman API Testing and Validation

A dedicated Postman collection was created for repeatable API validation.

### 14.1 Postman Artifacts

```text
postman/
├── CARIVIX_AI.postman_collection.json
└── CARIVIX_AI.postman_environment.json

run_postman_api_tests.py

reports/
└── postman_api_test_results.json
```

### 14.2 Test Coverage

The collection contains **15 test cases** covering:

| # | Test Case |
|---|---|
| 1 | Health |
| 2 | Model listing |
| 3 | Model information |
| 4 | Default prediction |
| 5 | RandomForest prediction |
| 6 | Batch prediction |
| 7 | RAG query |
| 8 | Context-based RAG |
| 9 | ML natural-language routing |
| 10 | Combined routing |
| 11 | Out-of-domain behavior |
| 12 | Empty-query validation |
| 13 | Invalid prediction validation |
| 14 | Root endpoint |
| 15 | OpenAPI specification |

### 14.3 Postman Result

| Metric | Value |
|---|---|
| Total Tests | 15 |
| Passed | 15 |
| Failed | 0 |
| Success Rate | 100%  |

---

## 15. Automated Regression and RAG Testing

### 15.1 Pytest Regression Testing

The complete pytest suite was executed.

| Metric | Value |
|---|---|
| Total Tests | 50 |
| Passed | 50 |
| Failed | 0 |
| Success Rate | 100%  |

**Test Distribution:**

| Test File | Tests Passed |
|---|---|
| `tests/test_api.py` | 10 |
| `tests/test_rag_pipeline.py` | 40 |

**The API tests validated:**

- Health
- Model listing
- Model information
- Prediction
- Batch prediction
- Error paths

**The RAG tests validated:**

- Document loading
- Chunking
- Embeddings
- FAISS storage
- Retrieval
- Prompt assembly

### 15.2 RAG Test-Set Evaluation

The RAG evaluation was executed using:

```bash
evaluate_rag.py --mode test-set
```

**Configuration:**

| Parameter | Value |
|---|---|
| Chunk Size | 300 |
| Overlap | 50 |
| Retrieval Top-k | 3 |

**Results:**

| # | Scenario | Score / Result | Status |
|---|---|---|---|
| 1 | Direct factual | 0.6878 | PASS  |
| 2 | Context based | 0.5202 | PASS  |
| 3 | Multi-document | 0.5344 | PASS  |
| 4 | Insufficient context | Correct refusal | PASS  |
| 5 | Source grounding | 0.4828 | PASS  |

**Total: 5 / 5 Passed** 

---

## 16. Latency and Performance Validation

### 16.1 Observed Latency

| Operation | Observed Latency |
|---|---|
| Health Check | 8.9 ms |
| Model Information | 27.5 ms |
| ML Prediction | 206.6–239.5 ms |
| Batch Prediction | 187.6 ms |
| FAISS Retrieval | 15.1–30.9 ms |
| RAG Cold Request | 25.20 sec |
| RAG Warm Requests | 4.86–8.05 sec |

### 16.2 API Performance

The health and metadata endpoints respond in milliseconds. This indicates that basic FastAPI routing and service-status operations have low overhead.

### 16.3 ML Performance

ML prediction latency was approximately **206.6–239.5 ms**.

This includes the API-to-model processing path, not only raw model computation.

### 16.4 RAG Performance

RAG has substantially higher latency:

| Condition | Latency |
|---|---|
| Cold | 25.20 seconds |
| Warm | 4.86–8.05 seconds |

The observed difference indicates that model initialization/loading and LLM generation contribute substantially to total response time.

FAISS retrieval itself was much faster: **15.1–30.9 ms**.

Therefore, vector retrieval is not the dominant latency component in the tested configuration.

---

## 17. Testing Artifacts and Repository Evidence

The Sprint 5 implementation produced reusable testing artifacts.

### 17.1 Postman Collection

`postman/CARIVIX_AI.postman_collection.json`

Contains the 15 API requests and test scenarios.

### 17.2 Postman Environment

`postman/CARIVIX_AI.postman_environment.json`

Stores local API configuration such as the base URL.

### 17.3 Automated Runner

`run_postman_api_tests.py`

Used to execute the Postman test specifications programmatically.

### 17.4 Raw Test Results

`reports/postman_api_test_results.json`

Contains execution information including responses and latency.

### 17.5 Detailed API Report

`reports/CARIVIX_AI_API_Testing_Report.md`

Contains the detailed testing report.

### 17.6 Additional Evaluation Evidence

The Sprint 5 work also included:

| # | Artifact |
|---|---|
| 1 | Updated RAG evaluation report |
| 2 | Re-indexed FAISS vector store |
| 3 | API regression results |
| 4 | Postman results |

These artifacts provide repeatability for future API validation.

---

## 18. Implementation Status, Gaps and Production Considerations

### 18.1 Currently Validated

| Metric | Value |
|---|---|
| Postman tests | 15 / 15 passed |
| Pytest tests | 50 / 50 passed |
| RAG evaluation cases | 5 / 5 passed |
| **TOTAL** | **70 / 70 passed** ✅ |
| Failures | 0 |
| Errors | 0 |
| Overall Pass Rate | 100% |

### 18.2 Important Integration Gaps

####  Natural-Language Feature Extraction

The ML models require structured features. The current AI endpoint correctly identifies when required fields are missing rather than inventing values.

A future enhancement can provide a controlled natural-language-to-feature extraction layer.

#### Combined ML/RAG Processing

Combined routing is operational from the API perspective, but complete automatic ML feature mapping should be treated as an area for further implementation.

####  RAG Latency

RAG warm requests remain significantly slower than direct ML prediction.

Potential areas for engineering optimization:

| # | Optimization Area |
|---|---|
| 1 | LLM initialization |
| 2 | Model caching |
| 3 | Prompt size |
| 4 | Generation parameters |
| 5 | Context size |
| 6 | Model selection |
| 7 | Response streaming |

####  Security

Before production exposure, the API should include:

| # | Security Control |
|---|---|
| 1 | Authentication |
| 2 | Authorization |
| 3 | HTTPS |
| 4 | Secret management |
| 5 | Rate limiting |
| 6 | Request logging |
| 7 | Input sanitization |
| 8 | Prompt-injection controls |

####  Monitoring

Production monitoring should track:

| # | Metric |
|---|---|
| 1 | API latency |
| 2 | ML inference latency |
| 3 | RAG retrieval latency |
| 4 | LLM generation latency |
| 5 | Model loading failures |
| 6 | Route distribution |
| 7 | Validation failures |
| 8 | RAG refusal rate |
| 9 | Retrieval quality |
| 10 | Model prediction failures |

### 18.3 Target Production Architecture

This represents the recommended production-oriented integration direction rather than claiming that every production control shown is already implemented.

```text
Client / Frontend
        ↓
HTTPS / Reverse Proxy
        ↓
Authentication + Authorization
        ↓
Rate Limiting + Request Logging
        ↓
FastAPI API Layer
        ↓
Input Sanitization + Validation
        ↓
NLP / AI Routing (+ prompt-injection controls)
        ↓
┌───────────────┼───────────────┐
↓               ↓               ↓
RAG             ML              Combined
        └───────┼───────┘
                ↓
        JSON API Response
                ↓
Monitoring / Observability
```

---

## 19. Conclusion and Final Integration Status

The CARIVIX AI API and module integration has progressed from individual ML/RAG components into a validated API-driven AI system.

### Current Integration Provides

```text
CARIVIX AI
    ↓
FastAPI Interface
    ↓
Validation Layer
    ↓
NLP / AI Routing
    ↓
┌───────────────┼───────────────┐
↓               ↓               ↓
RAG             ML              Combined
↓               ↓               ↓
FAISS           Models          RAG + ML
↓               ↓               ↓
LLM             Prediction      Response
└───────────────┼───────────────┘
                ↓
            JSON API
```

### Validation Evidence

| Metric | Result |
|---|---|
| Postman tests | 15 / 15 passed |
| Pytest tests | 50 / 50 passed |
| RAG evaluation cases | 5 / 5 passed |
| **Total Tests** | **70 / 70 passed** ✅ |
| Observed Pass Rate | 100% |
| Failures | 0 |
| Errors | 0 |

### The API Successfully Validated

| # | Capability |
|---|---|
| 1 | Service health |
| 2 | Model availability — eight ML models |
| 3 | Single prediction |
| 4 | RandomForest prediction |
| 5 | Batch prediction |
| 6 | RAG retrieval |
| 7 | Context-based generation |
| 8 | ML route selection |
| 9 | Combined route selection |
| 10 | Out-of-domain refusal |
| 11 | Input validation |
| 12 | OpenAPI documentation |

### Performance Characteristics

| Operation | Latency Range |
|---|---|
| Direct ML inference | ~206–240 ms |
| FAISS retrieval | ~15–31 ms |
| RAG warm requests | ~4.86–8.05 seconds |
| RAG cold request | ~25.20 seconds |

This indicates that LLM/model initialization and generation are the major areas for future latency optimization.

### Reusable Validation Artifacts

The following artifacts provide reusable validation for subsequent development cycles:

- Postman collection
- Postman environment
- Automated test runner
- Raw test results
- API testing report
- Updated RAG evaluation evidence
- Re-indexed FAISS store

### Next-Level Engineering Areas

| # | Area |
|---|---|
| 1 | Natural-language feature extraction for ML |
| 2 | Deeper combined RAG/ML orchestration |
| 3 | RAG latency optimization |
| 4 | Production security |
| 5 | Observability |
| 6 | Continued automated regression testing |

> **Final Sprint 5 Integration Status:** API and module integration validated successfully with **70/70** recorded tests passing. ✅

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-19 | Shivanath Samudrala | Initial version — API and module integration documentation |
