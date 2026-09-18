---
title: "CARIVIX AI — Backend Architecture"
document_id: "PY-02"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# CARIVIX AI — Backend Architecture

## 1. Overview

The CARIVIX AI backend is organized into **four core services**.

| Service | Status |
|---|---|
| Data Ingestion Service |  Fully connected |
| Processing Workflow Service |  Fully connected |
| Database Service |  Fully connected |
| Predictive Analytics |  Functions only — not yet wrapped into a service |

> **Summary:** Three of them are fully connected and share a **consistent design pattern**. The fourth exists as a **set of functions** but has **not yet been wrapped into a service** of its own.

---

## 2. Data Ingestion Service

This service handles pulling data into the system from **four source types**:

| # | Source Type |
|---|---|
| 1 | CSV files |
| 2 | Excel files |
| 3 | JSON files |
| 4 | External APIs |

### Key Design Points

- All four source types are accessed through **one common entry point**, so calling code does not need to know which importer to use for a given source
- Before any data is fetched, the service **validates the request**:
  - Checks that the source category is valid
  - Checks that the requested source name actually exists in the configuration
- If either check fails, a **clear error is returned immediately** rather than attempting the fetch

---

## 3. Processing Workflow Service

This service takes raw data and runs it through a **full cleaning and transformation sequence**.

### Processing Steps

| # | Step |
|---|---|
| 1 | Removing duplicate rows |
| 2 | Standardizing column names and text values |
| 3 | Handling missing values |
| 4 | Converting non-numeric values in numeric columns into a consistent missing value marker |
| 5 | Normalizing numeric columns |
| 6 | Encoding categorical columns |
| 7 | Applying memory optimizations to reduce the size of the resulting dataset |

### Configuration-Based Mode

The service also supports a **configuration-based mode**, where a **named profile** defines which columns should be:

- Normalized
- Encoded
- Treated as dates

> This allows the **same processing logic to be reused across different datasets** without repeating column-level instructions each time.

**Available profiles:**

- Defined in a configuration file
- Can be **extended without changing any application code**

---

## 4. Database Service

This service manages **all interaction with the underlying database**.

### Responsibilities

| # | Responsibility |
|---|---|
| 1 | Opening and closing connections |
| 2 | Writing single records or batches of records |
| 3 | Reading records back with optional filtering |
| 4 | Returning clear errors if an operation fails |

> **Design principle:** Rather than exposing **raw low-level database errors** to the caller, the service returns **clear, controlled errors**.

### Current Implementation

- Uses a **single fixed database file**
- Does **not** support multiple configurable databases

---

## 5. Predictive Analytics

This includes forecasting functions such as:

| # | Function |
|---|---|
| 1 | Moving average forecasting |
| 2 | ARIMA-based forecasting |
| 3 | Growth rate calculations |

### Current Status

| Aspect | Status |
|---|---|
| Functions exist |  Yes |
| Functions tested |  Yes |
| Wrapped into a connected service |  Not yet |
| Reachable through the API |  Not yet |

> **This is expected future work.**

---

## 6. Shared Design Pattern

Each of the **three connected services** follows the **same structure**.

| # | Pattern Element | Description |
|---|---|---|
| 1 | **Clear Entry Point** | Each service has one clear entry point, rather than requiring the caller to work with several smaller functions directly |
| 2 | **Logging** | Each logs its own operations, including what was requested and whether it succeeded or failed |
| 3 | **Error Handling** | Each raises a specific, named error type when something goes wrong, rather than letting an unrelated technical error surface to the caller |

---

## 7. Known Limitations

### 7.1 No Authentication

> The API currently has **no authentication or access control**.

Any system that can reach the server can call **any endpoint**, including writing to and reading from the database.

**Status:** Should be treated as a **development environment only** until access control is added.

### 7.2 Single Database File

> The database used by the API is a **single fixed file** rather than a configurable connection.

All stored data currently lives in **one place**.

### 7.3 Predictive Analytics Not Exposed

> Predictive analytics functions are **not yet exposed through the API** and can only be accessed **directly in Python**.

---

## 8. Testing

All **four services**, along with the **API layer built on top of them**, are covered by an automated test suite.

| Test Type | Description |
|---|---|
| **Total Tests** | 69 |
| **Invalid Data Tests** | Checks behavior with invalid data |
| **End-to-End Tests** | Checks the full workflow from ingestion through to storage |
| **Concurrency Tests** | Confirms the database service handles multiple simultaneous write requests correctly |

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — backend architecture |
