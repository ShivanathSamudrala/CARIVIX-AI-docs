---
title: "Correlation Analysis"
document_id: "DA-07"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# Correlation Analysis

## 1. Overview

Correlation analysis was performed to identify statistical associations between numerical indicators across the analytical datasets. The work progressed across Sprint 3 and Sprint 4, moving from initial eligible-relationship analysis to a comprehensive multi-dataset correlation study.

| Sprint | Focus |
|---|---|
| Sprint 3 | Initial Correlation Analysis |
| Sprint 4 | Expanded Correlation Analysis |

---

## 2. Sprint 3 — Initial Correlation Analysis

Sprint 3 performed correlation analysis for **eligible dataset relationships**.

### Work Performed

| # | Activity |
|---|---|
| 1 | Identifying numerical relationships |
| 2 | Screening dataset pairs |
| 3 | Excluding relationships where required dimensions were unavailable |
| 4 | Documenting relationship results |

> The Sprint 3 analysis resulted in **10 eligible relationships** being analyzed.

---

## 3. Sprint 4 — Expanded Correlation Analysis

Sprint 4 expanded the correlation analysis across a wider set of indicators and datasets.

### Results

| Metric | Value |
|---|---|
| Relationship pairs analyzed | 138 |
| Key correlation patterns | 25 |
| Significant insights | 25 |
| High-priority insights | 13 |
| Medium-priority insights | 12 |
| Positive relationships | 19 |
| Negative relationships | 6 |

---

## 4. Important Correlations

| Indicator 1 | Indicator 2 | Correlation |
|---|---|---|
| Active Jobcard Rate % | Worker Participation Rate % | 0.9941 |
| Wage Share % | Material Cost Share % | −0.5982 |
| Wage Share % | Administrative Cost Share % | −0.5660 |
| SC Participation Rate % | ST Participation Rate % | −0.4896 |
| Active Jobcard Rate % | ST Participation Rate % | 0.4274 |

---

## 5. Interpretation

Correlation analysis identifies **statistical association** between variables.

> **It does not establish causation.**

### Note on Derived Variables

Derived variables such as **Previous Value** and **Absolute Change** can produce **strong mathematical correlations** because they are calculated from related underlying values.

> Such relationships were therefore considered **carefully during interpretation** — high correlation between derived variables does not necessarily reflect an independent real-world relationship.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — correlation analysis |
