---
title: "AI Evaluation Process"
document_id: "ML-04"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Nerella Raghavendra Guptha
Role: ML & AI Engineer
---

# AI Evaluation Process

## 1. Evaluation Overview

The CARIVIX AI Evaluation Process is designed to determine whether the AI/ML and RAG components are producing **relevant, factually supported, reliable, and sufficiently fast** results.

Successful execution of the AI pipeline alone is **not** considered sufficient evidence of quality. An AI pipeline can execute successfully while still producing:

- Irrelevant retrieval results
- Incomplete context
- Incorrect predictions
- Unsupported statements
- Hallucinated information
- Poorly grounded answers
- Incorrect intent classification
- High response latency
- Integration errors

Therefore, evaluation is treated as a **separate engineering stage after implementation**.

The CARIVIX evaluation process focuses primarily on the RAG and AI response pipeline while also providing a framework for evaluating the interaction between query processing, retrieval, LLM generation, and API services.

### Overall Evaluation Objectives

| # | Objective |
|---|---|
| 1 | Verify that the correct information is retrieved |
| 2 | Verify that retrieved information is relevant to the query |
| 3 | Verify that the generated response addresses the user's question |
| 4 | Verify that factual statements are supported by retrieved context |
| 5 | Detect unsupported or hallucinated information |
| 6 | Measure response latency |
| 7 | Identify pipeline-level failures |
| 8 | Compare results before and after improvements |
| 9 | Establish repeatable evaluation criteria |
| 10 | Provide evidence for further AI/RAG optimization |

---

## 2. Evaluation Scope

The CARIVIX AI evaluation process covers the major stages of the AI/RAG workflow.

**Evaluation scope includes:**

- Query processing
- Document retrieval
- Embedding generation
- Vector search
- Top-K retrieval
- Context construction
- Prompt processing
- LLM response generation
- Response relevance
- Response factuality
- Groundedness
- Latency
- Failure analysis
- API-level behavior

### Two Major Evaluation Areas

| Area | Purpose |
|---|---|
| **A. Retrieval Evaluation** | Determines whether the system finds the correct information |
| **B. Generation Evaluation** | Determines whether the LLM uses that information correctly to produce the final answer |

> **This distinction is critical.**

**Example:**

If a user asks:

> "What is the documented embedding model?"

- If the correct document chunk is **never retrieved** → primary problem is **retrieval**
- If the correct chunk **is retrieved** and clearly states the embedding model but the LLM gives a different answer → primary problem is **generation, prompt handling, or grounding**

---

## 3. AI Evaluation Pipeline

The complete evaluation process follows a controlled sequence.

1. Create a test set containing representative user queries
2. Each test query should have an expected answer or expected evidence
3. Pass the query through the complete RAG pipeline
4. System performs:
   - Query processing
   - Query embedding
   - Vector search
   - Top-K retrieval
   - Context construction
   - Prompt generation
   - LLM inference
   - Response generation
5. Compare the resulting output against the expected information

### Iterative Evaluation Cycle

```text
Test
    → Measure
    → Identify Failure
    → Improve
    → Re-test
    → Compare Results
```

This creates an **iterative evaluation cycle** rather than a one-time test.

---

## 4. Test Dataset and Evaluation Set Creation

A reliable evaluation process requires a controlled test dataset. The evaluation test set should represent the types of questions the CARIVIX AI engine is expected to process.

### Question Categories

| Category | Description |
|---|---|
| **Knowledge Retrieval Questions** | Answers exist directly inside the indexed documents |
| **Document Summary Questions** | Require the system to summarize retrieved information |
| **Specific Fact Questions** | Require a precise factual answer |
| **Multi-context Questions** | Require information from more than one retrieved section |
| **Insufficient-Context Questions** | Required information is not present in available documents |
| **Ambiguous Questions** | Could potentially refer to multiple concepts |

The test set should contain enough variation to expose weaknesses in retrieval and generation.

### Evaluation Record Structure

| Field | Description |
|---|---|
| Test ID | Unique identifier for the test |
| User Query | User's test question |
| Expected Information | Information that should be retrieved |
| Expected Source / Document | Document expected to contain the answer |
| Expected Relevant Context | Context expected to be relevant |
| Retrieved Context | Context actually returned |
| Generated Response | AI-generated answer |
| Retrieval Result | Retrieval evaluation outcome |
| Grounding Result | Grounding evaluation outcome |
| Factuality Result | Factuality evaluation outcome |
| Latency | Measured response time |
| Failure Type | Category of failure (if applicable) |
| Final Evaluation Status | Overall pass / partial / fail |

### Semantic vs Exact Match

The expected answer should **not** always be treated as a fixed sentence. For RAG evaluation, the important requirement is often the **expected factual content or evidence** rather than exact wording.

**Example:**

| Type | Content |
|---|---|
| Expected Information | "Embedding model = all-MiniLM-L6-v2" |
| Generated Response | "The CARIVIX RAG pipeline uses all-MiniLM-L6-v2 for generating embeddings." |
| Verdict | ✅ Semantically correct even though the wording differs |

---

## 5. Retrieval Evaluation

Retrieval evaluation measures whether the vector-search layer is returning useful information.

### Documented RAG Architecture

| Parameter | Value |
|---|---|
| Embedding Model | SentenceTransformers all-MiniLM-L6-v2 |
| Embedding Dimension | 384 |
| Vector Search | FAISS L2 |
| Retrieval Type | Top-K |

### Retrieval Evaluation Should Determine

- Whether the expected document was retrieved
- Whether the expected chunk was retrieved
- How high the relevant chunk appears in the ranking
- How much irrelevant content is included
- Whether the retrieved context is sufficient to answer the query

### Important Retrieval Concepts

| Concept | Description |
|---|---|
| **Top-K Retrieval** | Number of chunks returned from vector search. Documented default: **K = 5** |
| **Precision-oriented Retrieval Analysis** | Measures how much of the retrieved content is relevant |
| **Recall-oriented Retrieval Analysis** | Measures whether the relevant information was successfully retrieved |
| **Rank-based Evaluation** | Measures where the relevant information appears in the retrieval ranking |

### Rank Example

| Rank | Meaning |
|---|---|
| Rank 1 | Highest retrieval priority |
| Rank 2 | Second result |
| Rank 3 | Third result |
| … | … |

> A relevant chunk appearing at **rank 1** is operationally different from the same chunk appearing at **rank 5**, because higher-ranked context is more likely to influence downstream generation.

### Retrieval Score Interpretation

The retrieval score must be interpreted according to the configured **FAISS distance/search mechanism**.

> A reported score such as approximately **0.72** should **not** be described as "72% accuracy" without a defined metric and evaluation methodology.

---

## 6. Context Quality Evaluation

Retrieval alone does not guarantee good RAG performance. The retrieved chunks must provide enough information for the LLM to answer the question.

### Context Evaluation Dimensions

| Dimension | Description |
|---|---|
| Relevance | Information directly related to the user's question |
| Completeness | Enough information to answer the question |
| Consistency | No internal contradictions |
| Duplication | Minimal repetition |
| Noise | Minimal irrelevant content |
| Source Alignment | Context matches the expected source |
| Context Size | Appropriate amount of text for the LLM |

### Impact of Poor Context

- **Irrelevant chunks** increase the amount of information the LLM must process and can introduce competing or confusing information
- **Incomplete context** can cause the LLM to produce an incomplete answer even when the correct document exists somewhere in the knowledge base

### Failure Classification

The evaluation should distinguish between:

| Failure Type | Meaning |
|---|---|
| Correct document **not** retrieved | Retrieval-level failure |
| Correct document retrieved but **insufficient context** | Context-quality failure |
| Correct context retrieved but **incorrect response** | Generation-level failure |

This classification helps determine **which part of the pipeline requires improvement**.

---

## 7. Response Relevance and Factuality

### Response Relevance

Response relevance determines whether the generated answer **actually addresses** the user's question. A response may be factually correct but still fail to answer the question directly.

**Example:**

| Field | Value |
|---|---|
| User asks | "What embedding model is used?" |
| System provides | A long explanation about FAISS without identifying the embedding model |
| Verdict | Technically correct information but **poor relevance** |

**Response evaluation checks:**

- Does the answer address the question?
- Does it contain the required information?
- Is unnecessary information minimized?
- Is the answer understandable?
- Does the response remain within the requested scope?

### Factuality

Factuality checks whether statements in the response are **consistent with the available evidence**.

**The evaluation should identify:**

- Correct statements
- Incorrect statements
- Unsupported statements
- Partially supported statements
- Contradictory statements

> For RAG, factuality must be evaluated against **retrieved evidence** rather than only against general model knowledge.

---

## 8. Groundedness Evaluation

Groundedness is one of the **most important evaluation dimensions** for CARIVIX RAG.

A response is considered grounded when its **project-specific factual claims** can be supported by the retrieved context.

### Evaluation Process

```text
User Query
    ↓
Retrieved Context
    ↓
Generated Response
    ↓
Identify Factual Claims
    ↓
Check Claims Against Context
    ↓
Grounded / Partially Grounded / Unsupported
```

### Grounded Example

| Field | Content |
|---|---|
| Retrieved Context | "Embedding model: all-MiniLM-L6-v2." |
| Generated Response | "The system uses all-MiniLM-L6-v2 to generate text embeddings." |
| Verdict | ✅ **Grounded** |

### Unsupported Example

| Field | Content |
|---|---|
| Generated Response | "The system uses a 1536-dimensional OpenAI embedding model." |
| Context Support | ❌ Not supported by retrieved context |
| Verdict | ⚠️ **Unsupported** |

The system should therefore be evaluated for **unsupported generation**.

> Groundedness evaluation is especially important because the purpose of RAG is **not simply to generate fluent text**. The purpose is to generate useful responses **based on retrieved evidence**.

---

## 9. End-to-End Evaluation and Latency

The complete AI/RAG system must also be evaluated as an **end-to-end pipeline**. The evaluation should measure the time required by each major stage.

### Latency Components

| Component | Description |
|---|---|
| Query Preprocessing Time | Time to normalize and prepare the query |
| Query Embedding Time | Time to convert query into a vector |
| FAISS Retrieval Time | Time for vector search |
| Context Construction Time | Time to assemble retrieved chunks |
| Prompt Construction Time | Time to build the final prompt |
| LLM Inference Time | Time for model to generate the response |
| Response Formatting Time | Time to format the output |
| **Total API Response Time** | End-to-end time |

> Latency should be recorded consistently under comparable conditions.

LLM generation can represent a significant part of total response time, particularly when running the model locally through Ollama. **Separating latency by component** helps determine whether performance improvements should target retrieval, embedding generation, prompt processing, or LLM inference.

---

## 10. Failure Analysis and Error Classification

When an evaluation fails, the failure should be **classified** rather than simply recorded as "wrong answer."

### Major Failure Categories

| # | Failure Category | Description |
|---|---|---|
| 1 | **Document Ingestion Failure** | Required document content was not correctly loaded |
| 2 | **Chunking Failure** | Relevant information was split incorrectly or contextual boundaries were lost |
| 3 | **Metadata Failure** | Required metadata was missing or incorrectly associated with a chunk |
| 4 | **Embedding Failure** | Text was not converted correctly into the required vector representation |
| 5 | **Vector Search Failure** | Relevant information was not returned by FAISS |
| 6 | **Retrieval Ranking Failure** | Relevant information was retrieved but ranked too low |
| 7 | **Context Construction Failure** | Retrieved information was not correctly passed into the prompt |
| 8 | **Prompt Failure** | The prompt did not sufficiently instruct the model to use the retrieved context |
| 9 | **LLM Generation Failure** | The model produced an incorrect or incomplete answer despite receiving useful context |
| 10 | **Grounding Failure** | The generated response contained claims that could not be supported by retrieved evidence |
| 11 | **API Integration Failure** | The AI output was not correctly returned through the API |
| 12 | **Latency Failure** | The response exceeded the acceptable performance target |

### Why Failure Classification Matters

Failure classification makes the evaluation **actionable**:

- If **retrieval fails** repeatedly → changing the prompt alone will not solve the underlying problem
- If **retrieval is correct but responses are unsupported** → prompt and generation behavior should be investigated
- If **responses are correct but slow** → performance optimization should focus on latency rather than answer quality

---

## 11. Evaluation Results, Iteration and Current Status

### Recommended Evaluation Record

| Field | Description |
|---|---|
| Test ID | Unique identifier for the test |
| Query | User's test question |
| Expected Evidence | Information that should be retrieved |
| Retrieved Evidence | Information actually returned |
| Retrieval Result | Relevant / Partially Relevant / Irrelevant |
| Response | Generated AI answer |
| Relevance | Pass / Partial / Fail |
| Factuality | Pass / Partial / Fail |
| Groundedness | Pass / Partial / Fail |
| Latency | Measured response time |
| Failure Type | If applicable |
| Action | Required improvement |
| Retest | Result after modification |

### Iterative Evaluation Example

```text
Baseline RAG
    ↓
Evaluate
    ↓
Identify poor retrieval
    ↓
Modify chunking or retrieval configuration
    ↓
Evaluate again
    ↓
Compare retrieval results
    ↓
Modify prompt if required
    ↓
Evaluate generation
    ↓
Measure groundedness
    ↓
Measure latency
    ↓
Finalize validated configuration
```

### Current Status

The latest CARIVIX implementation work includes testing the RAG indexing and query execution through the documented `main_rag.py` workflow.

A test query produced a relevant top retrieval with a reported score around **0.72**.

> This is evidence that the retrieval workflow is executing and returning a relevant result **for that test case**. However, this single result is **not sufficient** to establish overall retrieval accuracy. A proper evaluation requires a **representative test dataset and defined metrics**.

---

## 12. Conclusion

The CARIVIX AI Evaluation Process provides a structured method for validating the reliability and quality of the AI/RAG system.

The evaluation process does **not** treat successful execution as the final objective. Instead, the complete pipeline is evaluated across:

- Retrieval quality
- Context quality
- Response relevance
- Factuality
- Groundedness
- Latency
- API integration
- Failure behavior

### Most Important Principle

> **Separate retrieval evaluation from generation evaluation.**

| Evaluation Type | Determines |
|---|---|
| **Retrieval Evaluation** | Whether the system finds the correct evidence |
| **Generation Evaluation** | Whether the LLM correctly uses that evidence |
| **Groundedness Evaluation** | Whether project-specific claims in the final response are supported by retrieved context |
| **Latency Evaluation** | Whether the complete pipeline can respond within an acceptable time |
| **Failure Analysis** | Connects evaluation results back to specific technical components (ingestion, chunking, embeddings, FAISS retrieval, prompt construction, LLM inference, API integration) |

### Iterative Engineering Loop

```text
IMPLEMENT
    → TEST
    → MEASURE
    → ANALYZE
    → IMPROVE
    → RETEST
    → VALIDATE
```

### Current Foundation

The current CARIVIX AI/RAG implementation has established the core components required for this evaluation framework:

- Document ingestion
- RecursiveCharacterTextSplitter-based chunking
- SentenceTransformers embeddings
- FAISS retrieval
- Context construction
- Prompt processing
- Ollama-based LLM inference
- RAG query execution

### Next Stage of Evaluation Maturity

- Expand the test set
- Define repeatable retrieval and response metrics
- Record latency at component level
- Perform systematic groundedness checks
- Classify failures
- Compare results across iterations to confirm measurable improvement
