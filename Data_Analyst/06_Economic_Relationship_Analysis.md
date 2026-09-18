---
title: "Economic Relationship Analysis"
document_id: "DA-06"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# Economic Relationship Analysis

## 1. Overview

The Economic Relationship Analysis work progressed across four sprints, moving from initial economic-indicator research to a comprehensive relationship and correlation analysis across the analytical datasets.

| Sprint | Focus |
|---|---|
| Sprint 1 | Economic Indicator Research |
| Sprint 2 | Economic Indicators and Derived Metrics |
| Sprint 3 | Relationship Analysis |
| Sprint 4 | Expanded Relationship Analysis |

---

## 2. Sprint 1 — Economic Indicator Research

Sprint 1 focused on **identifying economic indicators** relevant to CARIVIX AI.

Indicators were mapped to:

| # | Mapping Category |
|---|---|
| 1 | Analytical categories |
| 2 | Descriptions |
| 3 | CARIVIX use cases |
| 4 | Example analytical questions |

---

## 3. Sprint 2 — Economic Indicators and Derived Metrics

Sprint 2 **calculated economic indicators and derived metrics** to support analytical and dashboard workflows.

This included:

- Growth-related measures
- Other domain-specific analytical measures

---

## 4. Sprint 3 — Relationship Analysis

Sprint 3 analyzed **eligible relationships** between analytical datasets.

### Documented Results

| Metric | Value |
|---|---|
| Eligible relationships | 10 |
| Public Program relationships excluded | 5 |

> **Reason for exclusion:** The Public Program dataset did not contain a usable **Year / Time dimension** for those comparisons.

---

## 5. Sprint 4 — Expanded Relationship Analysis

Sprint 4 expanded the analysis substantially.

### Results

| Metric | Value |
|---|---|
| Relationship pairs | 138 |
| Key relationships | 31 |
| — Strong | 13 |
| — Moderate | 18 |
| — Positive | 24 |
| — Negative | 7 |

---

## 6. Selected Relationships

| Indicator 1 | Indicator 2 | Correlation |
|---|---|---|
| Active Jobcard Rate % | Worker Participation Rate % | 0.9941 |
| Wage Share % | Material Cost Share % | −0.5982 |
| Wage Share % | Administrative Cost Share % | −0.5660 |
| SC Participation Rate % | ST Participation Rate % | −0.4896 |
| Active Jobcard Rate % | ST Participation Rate % | 0.4274 |

---

## 7. Interpretation Note

> These values describe **statistical relationships** in the analyzed datasets.
>
> They **should not be interpreted as evidence of causation**.

Correlation indicates that two indicators move together (positively or negatively) within the analyzed data — it does not establish that one indicator causes the other. Any causal interpretation would require additional domain analysis, control variables, and statistical testing beyond correlation.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — economic relationship analysis |
