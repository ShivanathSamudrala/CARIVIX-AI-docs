---
title: "Prompt Templates"
document_id: "ML-05"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Nerella Raghavendra Guptha
Role: ML & AI Engineer
---

# Prompt Templates

## 1. Overview

Prompt templates are a structured mechanism used by the CARIVIX AI/RAG Engine to control how retrieved information, user queries, system instructions, and contextual information are provided to the Large Language Model (LLM).

In a Retrieval-Augmented Generation workflow, the LLM should **not** receive only the original user question. It should receive a **controlled prompt** containing the relevant retrieved context along with instructions that define how the response should be generated.

The prompt-template layer therefore acts as an **intermediate control layer** between the retrieval pipeline and the LLM inference layer.

### General Flow

```text
User Query
    → Retrieval
    → Retrieved Context
    → Prompt Construction
    → LLM
    → Grounded Response
```

The prompt template is responsible for converting these inputs into a **consistent model-ready instruction**.

### Conceptual RAG Prompt Structure

```text
System Instructions
    +
Retrieved Context
    +
User Question
    ↓
Prompt Template
    ↓
Formatted LLM Prompt
    ↓
LLM Inference
    ↓
Grounded Response
```

The objective is to ensure that the LLM generates answers using the **retrieved project or document information** instead of relying unnecessarily on unsupported knowledge.

---

## 2. Purpose of Prompt Templates

The primary purpose of prompt templates is to **standardize communication** between the RAG pipeline and the LLM.

Without a structured template, every query could potentially be sent to the model using different instructions, making responses inconsistent and difficult to evaluate.

### The Prompt-Template Layer Provides

| # | Benefit |
|---|---|
| 1 | Consistent system instructions |
| 2 | Consistent placement of retrieved context |
| 3 | Clear separation between context and user question |
| 4 | Controlled response-generation behavior |
| 5 | Grounding instructions for retrieved information |
| 6 | Better protection against unsupported answers |
| 7 | Easier testing and evaluation |
| 8 | Easier modification of prompting strategies |
| 9 | Reusable templates for different AI tasks |

For CARIVIX, this is particularly important because the **same AI infrastructure** can support document question answering, analysis, summarization, trend interpretation, and other intelligence workflows.

---

## 3. Prompt Template Architecture

The prompt-template architecture consists of several logical components.

### 3.1 System Instruction

The system instruction defines the behavior expected from the LLM.

It can specify that the model should:

- Use retrieved context
- Answer the user's question directly
- Avoid unsupported claims
- Indicate when sufficient information is unavailable
- Maintain a professional technical response style

### 3.2 Retrieved Context

The retrieval layer provides the relevant document chunks returned by the vector-search process.

The context can contain:

```text
Context 1
Context 2
Context 3
...
Context K
```

The retrieved information is **inserted into the prompt before LLM inference**.

### 3.3 User Query

The original user question is passed **separately** so that the LLM can distinguish:

- The information it needs to answer (the question)
- The supporting evidence (the context)

### 3.4 Response Instructions

Additional instructions can define the expected response format.

**Example:**

```text
Answer using only the supplied context.
If the context does not contain sufficient information,
state that the information is unavailable.
```

---

## 4. Prompt Construction Flow

The CARIVIX prompt construction process begins **after retrieval has completed**.

### Step-by-Step Flow

| Step | Action |
|---|---|
| 1 | User submits a query to the AI engine |
| 2 | Query is converted into an embedding using the configured embedding model |
| 3 | Vector representation is compared with vectors stored in the FAISS index |
| 4 | Retrieval layer returns the most relevant document chunks |
| 5 | Chunks are combined into a **context block** |
| 6 | Prompt-template layer combines System Instruction + Retrieved Context + User Query + Response Instruction |
| 7 | Resulting prompt is passed to the configured LLM inference layer |
| 8 | LLM processes the prompt and produces the final response |

This design keeps **retrieval and generation logically separated** while allowing the retrieved information to influence the generation stage.

---

## 5. Base RAG Prompt Template

A generic CARIVIX RAG prompt can be structured as follows:

```text
You are an AI assistant for the CARIVIX AI platform.

Use the following retrieved context to answer the user's question.

Retrieved Context:
{context}

User Question:
{question}

Instructions:
- Use the retrieved context as the primary source of information.
- Answer the question clearly and accurately.
- Do not introduce unsupported information.
- If the retrieved context does not contain enough information,
  clearly state that sufficient information is not available.

Answer:
```

### Dynamic Variables

| Variable | Populated By |
|---|---|
| `{context}` | Results returned from the retrieval pipeline |
| `{question}` | User's original query |

This makes the template **reusable across multiple requests**.

---

## 6. Context Formatting

Retrieved chunks should be formatted in a way that allows the LLM to distinguish individual pieces of evidence.

### Example

```text
Retrieved Context:

[Document 1]
Title: Economic Trend Analysis
Content:
Economic growth increased during the analyzed period...

[Document 2]
Title: Market Analysis
Content:
The market demonstrated increasing demand...

[Document 3]
Title: Public Program Evaluation
Content:
The program produced measurable improvements...
```

### Benefits of Structured Context Formatting

| # | Benefit |
|---|---|
| 1 | Improves readability for the LLM |
| 2 | Preserves boundaries between retrieved chunks |
| 3 | Makes debugging easier (developers can inspect exactly what was supplied) |
| 4 | Enables optional metadata inclusion for document-level traceability |

### Metadata Example

```text
Source: economic_trends.csv
Chunk ID: 12
Content:
...
```

> The exact metadata included in the final prompt should depend on the **implementation** and **token constraints**.

---

## 7. Grounded Response Template

A grounded-response template is designed to **reduce unsupported generation**.

**Example:**

```text
You are a CARIVIX AI assistant.

Answer the question using only the information contained
in the retrieved context.

Context:
{context}

Question:
{question}

Rules:
- Use the provided context as the primary evidence.
- Do not invent facts that are not supported by the context.
- Do not assume missing information.
- If the context is insufficient, state that explicitly.
- Provide a concise and technically accurate answer.

Response:
```

### Why This Matters

The important property of this template is the **explicit grounding instruction**. The model is not simply asked to answer the question — it is instructed to use the **retrieved evidence** as the basis for its response.

This is important for document intelligence because the objective of RAG is **not simply text generation** — it is **contextual generation based on retrieved information**.

---

## 8. Prompt Template Variables

The template system should keep **dynamic values** separate from **static instructions**.

### Core Variables

```text
{question}
{context}
```

### Optional Variables

| Variable | Purpose |
|---|---|
| `{conversation_history}` | Previous turns in multi-turn interactions |
| `{document_name}` | Name of the source document |
| `{metadata}` | Additional document-level metadata |
| `{response_format}` | Required output format |
| `{task_type}` | Task classification (QA, summary, analysis, etc.) |

### Example With Additional Variables

```text
System:
You are a document-analysis assistant.

Document:
{document_name}

Context:
{context}

Question:
{question}

Required Format:
{response_format}
```

Using variables allows the **same template** to support multiple requests without modifying the underlying prompt structure. This also makes **prompt testing easier** because different context and query values can be inserted into the same template.

---

## 9. Prompt Templates for Different AI Tasks

The CARIVIX architecture can use **task-specific prompt templates** while keeping the same underlying RAG architecture.

### 9.1 Question Answering

```text
Use the retrieved context to answer the following question.

Context:
{context}

Question:
{question}

Answer:
```

### 9.2 Summarization

```text
Summarize the following retrieved information.

Context:
{context}

Provide a concise summary containing the
most important information.

Summary:
```

### 9.3 Analysis

```text
Analyze the information provided in the context.

Context:
{context}

Question:
{question}

Identify the relevant patterns, relationships,
and observations supported by the context.

Analysis:
```

### 9.4 Comparison

```text
Compare the entities or concepts requested by the user.

Context:
{context}

Question:
{question}

Present the comparison using only information
supported by the retrieved context.

Comparison:
```

### 9.5 Trend Interpretation

```text
Analyze the trend information contained in the context.

Context:
{context}

Question:
{question}

Describe the observed trend and supporting evidence.

Trend Analysis:
```

> These templates can share the **same retrieval pipeline** while changing the **generation instructions** according to the requested task.

---

## 10. Prompt Construction Technical Diagram

The following represents the relationship between the user query, retrieval pipeline, prompt-template layer, and LLM:

```text
User Query
    ↓
Query Embedding
    ↓
FAISS Retrieval
    ↓
Retrieved Chunks
    ↓
Context Formatting
    ↓
Prompt Template Layer
    ↓
Formatted LLM Prompt
    ↓
Ollama / Llama 3.1
    ↓
Grounded Response
```

This architecture demonstrates that **prompt construction occurs after retrieval and before LLM inference**. The prompt template therefore acts as the **interface** between the retrieval subsystem and the generation subsystem.

---

## 11. Prompt Generation and LLM Integration

The prompt-template layer can be logically represented as:

```text
Prompt =
    System Instructions
    + Retrieved Context
    + User Question
    + Generation Instructions
```

The generated prompt is then supplied to the LLM.

For the CARIVIX implementation, the LLM inference layer is associated with the **local Ollama-based model-serving architecture**.

### Architectural Principle

> The prompt-template layer should remain **independent from the model implementation** wherever possible. This means that **changing the LLM should not require redesigning the entire RAG pipeline**.

**Example flow:**

```text
FAISS Retrieval
    ↓
Prompt Template
    ↓
Ollama
    ↓
Llama-based Model
```

---

## 12. Prompt Validation and Evaluation

Prompt templates should be evaluated as part of the AI evaluation process.

### Evaluation Areas

| Area | Purpose |
|---|---|
| **Relevance** | Response should directly address the user question |
| **Groundedness** | Generated answer should be supported by retrieved context |
| **Factuality** | Response should avoid unsupported or fabricated information |
| **Context Utilization** | Model should appropriately use retrieved chunks instead of ignoring them |
| **Response Quality** | Final answer should be understandable, technically appropriate, and aligned with the requested task |
| **Prompt Consistency** | Equivalent queries should receive responses generated using the same structural instructions |

### Basic Evaluation Workflow

```text
Test Query
    ↓
Retrieve Context
    ↓
Generate Prompt
    ↓
LLM Response
    ↓
Evaluate Response
    ↓
Relevance / Groundedness / Factuality
```

---

## 13. Prompt Lifecycle and Optimization

The prompt lifecycle demonstrates how prompt templates can be **developed, tested, evaluated, and integrated** into the production RAG pipeline.

### Prompt Lifecycle

```text
Draft Prompt Template
    ↓
Test with Sample Queries
    ↓
Evaluate Response Quality
    ↓
Modify Prompt / Instructions
    ↓
Re-test
    ↓
Compare Results
    ↓
Integrate into Production RAG Pipeline
```

> This represents **prompt engineering as an iterative engineering process** rather than a one-time activity. Prompt changes can be evaluated using predefined test cases before being integrated into the main AI pipeline.

---

## 14. Conclusion

Prompt templates provide the **control mechanism** required to connect the CARIVIX retrieval subsystem with the LLM generation subsystem in a consistent and structured manner.

The template combines:

- System instructions
- Retrieved document context
- The user's query
- Response-generation rules

…into a single **model-ready prompt**.

### Summary Flow

```text
User Query
    ↓
Query Embedding
    ↓
FAISS Retrieval
    ↓
Relevant Document Chunks
    ↓
Context Formatting
    ↓
Prompt Template
    ↓
LLM Inference
    ↓
Grounded Response
```

A structured prompt-template architecture improves:

- **Consistency**
- **Maintainability**
- **Grounding**
- **Testing**
- **Evaluation** of AI-generated responses

The design also provides flexibility for different AI operations such as question answering, summarization, analysis, comparison, and trend interpretation — while keeping the underlying **retrieval infrastructure reusable**.

> **Prompt templates should therefore be treated as an important component of the CARIVIX AI/RAG implementation** rather than as simple text instructions. They form the **controlled interface** through which retrieved knowledge is transformed into an LLM-generated response.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Nerella Raghavendra Guptha | Initial version — prompt templates documentation |
