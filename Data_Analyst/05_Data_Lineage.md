---
title: "Data Lineage and Traceability"
document_id: "DA-05"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# Data Lineage and Traceability

## 1. Overview

Data lineage and traceability define how data moves from its original source through cleaning, standardization, analytical processing, and dashboard consumption — while preserving evidence that the processed datasets remain faithful to their sources.

| Sprint | Focus |
|---|---|
| Sprint 1 | Source Identification and Documentation |
| Sprint 2 | Consolidation, Standardization, Analytical Outputs |
| Sprint 3 | Source-to-Processed Validation |
| Sprint 4 | Source-to-Target Lineage Validation |

---

## 2. Overall Data Flow

The Data Analyst workflow developed progressively across the sprints.

```text
Source Data
    ↓
Dataset Collection
    ↓
Data Cleaning
    ↓
Standardization
    ↓
Analytical Dataset
    ↓
Derived Indicators
    ↓
KPI Calculations
    ↓
Power BI Dashboard
    ↓
Validation
```

---

## 3. Sprint 1 — Source Identification

The focus was on:

- Identifying reliable data sources
- Documenting source information

---

## 4. Sprint 2 — Consolidation and Standardization

The team:

- Consolidated datasets
- Standardized datasets
- Created analytical outputs

---

## 5. Sprint 3 — Source-to-Processed Validation

Source-to-processed validation was completed.

### Final Validation Results

| Metric | Value |
|---|---|
| Comparable records | 470,332 |
| Matched values | 470,332 |
| Mismatches | 0 |
| Match rate | 100% |

**Lineage Summary:**

```text
470,332 comparable records
    → 470,332 matches
    → 0 mismatches
    → 100% match rate
```

---

## 6. Sprint 4 — Source-to-Target Lineage Validation

Sprint 4 completed **source-to-target lineage validation** for the six AI/ML-ready datasets.

### Lineage Verification Scope

The lineage process verified:

| # | Verified Element |
|---|---|
| 1 | Source dataset |
| 2 | Analytical dataset |
| 3 | Record counts |
| 4 | Dataset structure |
| 5 | Values |
| 6 | Data-quality characteristics |
| 7 | Derived fields |
| 8 | Final dashboard usage |

> The Sprint 4 documentation confirms that **processed datasets preserved** the expected record counts, structures, values and data-quality characteristics.

---

## 7. Lineage Flow for Dashboard KPIs

```text
Source Dataset
    ↓
Source Column
    ↓
Calculation / Aggregation
    ↓
KPI Measure
    ↓
Dashboard Page
    ↓
Dashboard Visual
    ↓
Validation
```

This flow provides **end-to-end traceability** from the original source column through to the final dashboard visual — allowing every KPI to be traced back to its underlying data.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — data lineage and traceability |
