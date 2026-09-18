---
title: "ML & AI Engineer — Evidence Links"
document_id: "ML-11"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# ML & AI Engineer — Evidence Links

## 1. Overview

This document consolidates all evidence, source materials, implementation references, session recordings, and technical artifacts supporting the **ML & AI Engineer** domain of the CARIVIX AI platform.

It provides direct links to:

- Source documents (Google Drive)
- Session recordings (Google Drive)
- Source code repository (GitHub)
- Technical diagrams and supporting assets
- Cross-references to formatted versions in this repository

This evidence trail supports **verification**, **reproducibility**, and **traceability** for all ML/AI work completed across Sprint 1 through Sprint 5.

---

## 2. Source Code Repository

The complete ML training and RAG pipeline implementation is maintained at:

🔗 **[github.com/Nerella-gupta/carivix-ai](https://github.com/Nerella-gupta/carivix-ai)**

### 2.1 Key Entry Points

| File | Purpose |
|---|---|
| `main.py` | Full ML training pipeline |
| `main_rag.py` | RAG pipeline CLI (`--index`, `--query`, `--interactive`, `--test`) |
| `api.py` | FastAPI server with integrated `/api/v1/ai/query` endpoint |
| `nlp_module.py` | NLP entrypoint (intent detection + routing) |
| `run_baseline_pipeline.py` | Baseline model comparison |
| `evaluate_rag.py` | RAG evaluation script |
| `mlflow.db` | MLflow experiment tracking database |

### 2.2 Module Directories

| Directory | Purpose |
|---|---|
| `rag/` | Modular RAG implementation (loader, splitter, embeddings, vector store, retriever, prompt builder, generator, pipeline) |
| `src/` | Core source modules |
| `config/` | Configuration files (`config.yaml`) |
| `data/` | Documents, raw data, processed data |
| `experiments/` | Baseline comparisons, model artifacts |
| `tests/` | Automated test suite |

### 2.3 Core Capabilities Implemented

**Model Training Pipeline:**

- Data loading & validation (CSV, Excel, Parquet)
- Data cleaning (missing values, duplicates, outliers, encoding, scaling, SMOTE/ADASYN)
- Feature engineering (polynomial, interaction, ratio, frequency, binning, clustering, PCA, text/date)
- Model training (8 classification + 9 regression algorithms)
- Hyperparameter tuning (GridSearchCV, RandomizedSearchCV)
- Cross-validation
- Model evaluation (accuracy, precision, recall, F1, ROC AUC / MAE, RMSE, R²)
- Experiment tracking via MLflow
- Model versioning & serialization

**RAG Pipeline:**

- Document loading (PDF, DOCX, TXT, CSV)
- Text preprocessing & semantic chunking (`RecursiveCharacterTextSplitter`)
- Embedding generation (Sentence Transformers `all-MiniLM-L6-v2`)
- FAISS vector indexing (L2 distance)
- Similarity retrieval (Top-K)
- Context-aware prompt construction
- LLM response generation (Ollama / Llama 3.1, Mistral, HuggingFace)

---

## 3. Source Documents (Google Drive)

All source `.docx` files for the ML/AI domain are available in the shared Drive folder:

🔗 **[CARIVIX AI — Documents](https://drive.google.com/drive/folders/14cnQTHOwJexWD3K9yaxo-XHtuYmXZkmW)**

### 3.1 Document Inventory

| # | Source Document | Date | Size | Formatted Version (Repo) |
|---|---|---|---|---|
| 1 | `AI & ML .docx` | Aug 24 | 640 KB | `01_Overview.md` |
| 2 | `AIRAG architecture.docx` | Sep 7 | 844 KB | `02_AI_RAG_Architecture.md` |
| 3 | `model workflow.docx` | Sep 7 | 642 KB | `03_Model_Workflow.md` |
| 4 | `AI Evaluation .docx` | Sep 7 | 715 KB | `04_AI_Evaluation_Process.md` |
| 5 | `Model Pipeline .docx` | Aug 22 | 1.2 MB | `05_Model_Pipeline.md` |
| 6 | `RAG Workflow.docx` | Sep 13 | 656 KB | `06_RAG_Workflow.md` |
| 7 | `Prompt Templates`  | Sep 18 | 662 KB | `08_Prompt_Templates.md` |
| 8 | `Grounded Responses`  | Sep 18 | 751 KB | `09_Grounded_Responses.md` |
| 9 | `AI Engine .docx` | Sep 17 | 781 KB | `09_AI_Engine.md` |
| 10 | `Prediction Engine.docx` | Sep 17 | 604 KB | `10_Prediction_Engine.md` |
| 11 | `CARIVIX AI Engine – AI Query Workflow.docx` | Aug 21 | 1.5 MB | `04_AI_Query_Workflow.md` |
| 12 | `Technical diagrams.docx` | Aug 24 | 1.4 MB | Diagrams 33–35 added to `09_Assets/` |
| 13 | `Task progress report - 17_09_2026.docx` | Sep 17 | 8 KB | Sprint 4 / 5 progress evidence |

> **Note:** Formatted versions in this repository preserve 100% of the source content while adding documentation-grade structure (frontmatter, numbered sections, tables, flow diagrams, version control).

---

## 4. Session Recordings (Google Drive)

All ML/AI working sessions, demos, and technical discussions are recorded and available in the shared Drive folder:

🔗 **[CARIVIX AI — Records](https://drive.google.com/drive/folders/1X6m6OGbF1P9pAiqAcUXXYMs99QB2BW_T)**

### 4.1 Recording Inventory

| # | Recording File | Date | Size |
|---|---|---|---|
| 1 | `Recording 2026-08-20 121438.mp4` | Aug 20, 2026 | 651.5 MB |
| 2 | `Recording 2026-08-20 174727.mp4` | Aug 20, 2026 | 155.2 MB |
| 3 | `Recording 2026-08-22 171133.mp4` | Aug 22, 2026 | 245.4 MB |

### 4.2 Purpose

These recordings serve as **primary evidence** of:

- Live implementation sessions
- Technical decision-making
- Architecture walkthroughs
- Sprint review discussions
- Team coordination on ML/AI deliverables

> Recordings are timestamped and preserved for **audit and verification purposes**.

---

## 5. Technical Diagrams

### 5.1 Diagrams Added to `09_Assets/`

The following technical diagrams were produced by the ML/AI Engineer and added to the shared asset library:

| # | Diagram | File |
|---|---|---|
| 33 | Document Metadata Handling | `09_Assets/33_Document_Metadata_Handling.md` |
| 34 | Prompt and Grounded Response | `09_Assets/34_Prompt_and_Grounded_Response.md` |
| 35 | AI Evaluation — RAG Metrics | `09_Assets/35_AI_Evaluation_RAG_Metrics.md` |

### 5.2 Source Diagram Set

The complete technical diagram set (Sprint 3 + Sprint 4) is documented in:

🔗 `Technical diagrams.docx` — [CARIVIX AI — Documents](https://drive.google.com/drive/folders/14cnQTHOwJexWD3K9yaxo-XHtuYmXZkmW)

**Sprint 3 — Architecture & Integration Diagrams:**

| # | Diagram |
|---|---|
| 01 | AI Architecture Integration |
| 02 | ML Pipeline |
| 03 | RAG Architecture |
| 04 | Document Processing |
| 05 | Embedding & Vector Search |
| 06 | LLM Integration |
| 07 | AI Component Integration |
| 08 | AI Technology Stack |
| 09 | End-to-End AI Workflow |
| 10 | AI Integration Readiness |

**Sprint 4 — Implementation & Evaluation Diagrams:**

| # | Diagram |
|---|---|
| 11 | RAG Implementation |
| 12 | Document Ingestion |
| 13 | Document Chunking |
| 14 | Metadata Handling  |
| 15 | Embedding & Retrieval |
| 16 | Retrieval Validation |
| 17 | Retrieval-to-LLM |
| 18 | Prompt & Grounded Response  |
| 19 | AI Evaluation  |
| 20 | Complete Sprint 4 AI Pipeline |

>   Promoted to `09_Assets/` as new files (33, 34, 35) — the other 17 overlap with existing diagrams.

---

## 6. Cross-Reference: ML Folder Documents

| # | Document | Repository Path | Source |
|---|---|---|---|
| 1 | Overview | `docs/07_ML_AI_Engineer/01_Overview.md` | `AI & ML .docx` |
| 2 | AI/RAG Architecture | `docs/07_ML_AI_Engineer/02_AI_RAG_Architecture.md` | `AIRAG architecture.docx` |
| 3 | Model Workflow | `docs/07_ML_AI_Engineer/03_Model_Workflow.md` | `model workflow.docx` |
| 4 | AI Evaluation Process | `docs/07_ML_AI_Engineer/04_AI_Evaluation_Process.md` | `AI Evaluation .docx` |
| 5 | Model Pipeline | `docs/07_ML_AI_Engineer/05_Model_Pipeline.md` | `Model Pipeline .docx` |
| 6 | RAG Workflow | `docs/07_ML_AI_Engineer/06_RAG_Workflow.md` | `RAG Workflow.docx` |
| 7 | Prompt Templates | `docs/07_ML_AI_Engineer/08_Prompt_Templates.md` | Source document |
| 8 | Grounded Responses | `docs/07_ML_AI_Engineer/09_Grounded_Responses.md` | Source document |
| 9 | AI Engine | `docs/07_ML_AI_Engineer/09_AI_Engine.md` | `AI Engine .docx` |
| 10 | Prediction Engine | `docs/07_ML_AI_Engineer/10_Prediction_Engine.md` | `Prediction Engine.docx` |
| 11 | Intern Contribution | `docs/07_ML_AI_Engineer/10_Intern_Contribution.md` | Intern learning report |

---

## 7. Sprint-wise Evidence Mapping

### Sprint 3 — Architecture & Integration

| Evidence Type | Artifact |
|---|---|
| Diagrams | Diagrams 01–10 (Sprint 3 set) |
| Source documents | `AI & ML .docx`, `AIRAG architecture.docx`, `Model Pipeline .docx` |
| Recordings | Aug 20 sessions |
| Code | Initial `rag/` module, `main_rag.py` |

### Sprint 4 — Implementation & Evaluation

| Evidence Type | Artifact |
|---|---|
| Diagrams | Diagrams 11–20 (Sprint 4 set) |
| Source documents | `AI Evaluation .docx`, `RAG Workflow.docx`, `model workflow.docx` |
| Recordings | Aug 22 session |
| Code | Enhanced RAG pipeline, FAISS integration, Ollama inference, evaluation scripts |

### Sprint 5 — Advanced Intelligence & Integration

| Evidence Type | Artifact |
|---|---|
| Source documents | `AI Engine .docx`, `Prediction Engine.docx` |
| Progress evidence | `Task progress report - 17_09_2026.docx` |
| Code | Full `api.py`, `nlp_module.py`, baseline pipeline |
| New diagrams | 33, 34, 35 added to `09_Assets/` |

---

## 8. Evidence Verification Checklist

| # | Evidence Category | Status | Location |
|---|---|---|---|
| 1 | Source code repository |  Available | GitHub |
| 2 | Source documents (13 files) |  Available | Google Drive — Documents |
| 3 | Session recordings (3 files) |  Available | Google Drive — Records |
| 4 | Technical diagrams (Sprint 3 + 4) |  Available | Drive + `09_Assets/` |
| 5 | Sprint progress report |  Available | Google Drive |
| 6 | Formatted repo documents |  Available | `docs/07_ML_AI_Engineer/` |
| 7 | RAG execution evidence (`main_rag.py`) |  Documented | Repo + source docs |
| 8 | MLflow experiment tracking |  Available | Repo (`mlflow.db`) |
| 9 | Test suite |  Available | Repo (`tests/`) |
| 10 | Evaluation framework |  Documented | `04_AI_Evaluation_Process.md` |

---

## 9. Repository Structure Cross-Reference

The following diagram shows how evidence is organized across the three primary locations:

```text
CARIVIX AI EVIDENCE
│
├── GitHub Repo (Source Code)
│   ├── main.py
│   ├── main_rag.py
│   ├── api.py
│   ├── rag/
│   └── mlflow.db
│
├── Google Drive (Documents)
│   ├── 13 .docx source files
│   ├── Diagrams
│   └── Reports
│
├── Repo (Docs)
│   ├── 01–11  ML .md files
│   └── 33–35  Assets
│
└── Google Drive (Records)
    └── 3 session recordings
```

---

## 10. Access and Permissions

| Resource | Access Level | Maintained By |
|---|---|---|
| GitHub Repository | Open / Public | Nerella Raghavendra Guptha |
| Google Drive — Documents | Shared with team | ML & AI Engineer |
| Google Drive — Records | Shared with team | ML & AI Engineer |
| Repo Documents (`docs/07_ML_AI_Engineer/`) | Shared with team | Technical Writer + ML & AI Engineer |

> **Note:** If you do not have access to any resource listed above, contact the ML & AI Engineer or the Technical Writing team.

---

## 11. Conclusion

This evidence document provides a **complete, traceable, and verifiable record** of the ML & AI Engineer's work across the CARIVIX AI platform.

**Coverage includes:**

-  Source code repository with full implementation
-  13 source documents (`.docx`) in Google Drive
-  3 session recordings in Google Drive
-  20 technical diagrams (Sprint 3 + 4)
-  3 new diagrams promoted to `09_Assets/`
-  11 formatted documents in `docs/07_ML_AI_Engineer/`
-  Sprint 5 progress report
-  RAG execution and evaluation evidence
-  MLflow experiment tracking

The evidence trail supports:

- **Reproducibility** of all ML/AI work
- **Verification** of claims made in technical documentation
- **Traceability** from source documents to formatted repo versions
- **Audit-readiness** for sprint reviews and stakeholder presentations

> **Key Principle:** Every claim in the ML/AI documentation should be traceable to a specific piece of evidence — source code, source document, diagram, recording, or execution result.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — ML & AI evidence links |
