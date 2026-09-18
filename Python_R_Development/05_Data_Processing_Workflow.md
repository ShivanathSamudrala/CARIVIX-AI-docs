---
title: "CARIVIX AI — Data Processing Workflow"
document_id: "PY-05"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# CARIVIX AI — Data Processing Workflow

## 1. Purpose

This document explains how raw data is **cleaned, transformed, and prepared for storage** within the CARIVIX AI backend.

It also covers the **technical approach** used to handle:

- Missing values
- Invalid data
- Inconsistent categories
- Different data types

…during processing.

---

## 2. Data Processing Workflow

The processing workflow performs **seven operations in a fixed order**. This ensures that each processing step receives data in the expected format **before moving to the next stage**.

### 2.1 Standardization

Column names and text values are first **standardized**. This handles differences in:

- Spacing
- Capitalization
- Formatting

…so that the same type of information follows **one consistent format** across the dataset.

### 2.2 Duplicate Removal

Duplicate rows are **identified and removed** based on the actual content of the records.

> This prevents repeated records from affecting further processing and analysis.

### 2.3 Numeric Value Validation

Columns identified as **numeric** are checked for values that **cannot be converted into numbers**.

**Example:** A text value appearing inside a revenue column is treated as an invalid numeric value.

> These values are **converted into a proper missing value marker** instead of causing the complete processing operation to fail.

### 2.4 Missing Value Handling

Missing values are handled using a **configurable strategy**.

> **Current default approach:** Fill missing values using the **median value** of the respective column.
>
> This provides a consistent way to handle gaps in numeric data during processing.

### 2.5 Numeric Normalization

Numeric columns can be **normalized** to bring values onto a **common scale**.

> This is useful when different numeric fields have significantly different ranges and the processed data is later used for **analysis or machine learning**.

### 2.6 Categorical Encoding

Categorical columns such as **region** or **category** are converted into a **numeric format**.

> This prepares categorical data for **downstream analysis and machine learning** processes that require numerical input.

### 2.7 Date Feature Extraction

When a date column is specified, additional date-based fields are **extracted automatically**.

**Extracted Features:**

| # | Feature |
|---|---|
| 1 | Year |
| 2 | Month |
| 3 | Day |
| 4 | Day of Week |
| 5 | Quarter |

> This provides downstream users with **ready-to-use date features** without requiring additional date processing.

---

## 3. Technical Issue Identified and Resolved

During early testing, an issue was identified in the **categorical encoding process**.

### Issue Description

> Categorical values with **different capitalization** were being treated as **separate categories**.

**Example:** The same category written in uppercase and lowercase could be encoded as **two different categories**.

**Impact:** This could result in one real category being **split into multiple encoded values** and could affect downstream analysis.

### Resolution

The processing logic was updated to:

1. **Standardize the casing** of categorical values
2. **Remove extra spaces** from categorical values before encoding

### Regression Prevention

> An **automated regression test** was also added to ensure that the same issue is **detected immediately** if it occurs again.

---

## 4. Reusable Configuration Profiles

The workflow supports **reusable configuration profiles** so that processing settings do not have to be defined manually for every dataset.

### Each Profile Can Specify

| # | Specification |
|---|---|
| 1 | Columns that require normalization |
| 2 | Columns that should be treated as categorical |
| 3 | The column that should be treated as a date |

### Currently Available Profiles

| # | Profile |
|---|---|
| 1 | Company Financial Data |
| 2 | Economic Indicator Data |

> **Additional profiles** can be added through the configuration file **without making changes to the application code**.

---

## 5. Performance and Scale

### Memory Optimization

The workflow includes a **memory optimization step** that adjusts data types to more efficient representations.

| Metric | Result |
|---|---|
| Memory Usage Reduction | **> 70%** on realistic sample data |

### Processing Performance

| Metric | Result |
|---|---|
| Dataset Size | 5,000 rows |
| Complete Workflow (all 7 steps) | **< 1 second**  |
| Measured Processing Rate | **~200,000 rows per second**  |

---

## 6. Realistic Data Testing

The workflow was tested using a **deliberately messy 500-row dataset**.

### Dataset Included

| # | Data Quality Challenge |
|---|---|
| 1 | Missing values |
| 2 | Invalid numeric values |
| 3 | Inconsistent category casing |
| 4 | Multiple variations of the same category |

### Test Results

| Result | Status |
|---|---|
| Complete dataset processed successfully | Completed |
| Data loss | **Zero**  |
| Inconsistent category values | Standardized and correctly combined before encoding  |

---

## 7. Processing Flow

The complete processing sequence is:

**Raw Data → Standardization → Duplicate Removal → Numeric Validation → Missing Value Handling → Numeric Normalization → Categorical Encoding → Date Feature Extraction → Processed Data**

> This fixed sequence ensures that data is **cleaned and transformed in a consistent manner** before being passed to the database or downstream services.

---

## 8. Summary

The Data Processing Workflow provides a **structured process** for preparing raw data for storage and further use.

### Handles Common Data Quality Issues

| # | Issue |
|---|---|
| 1 | Duplicates |
| 2 | Missing values |
| 3 | Invalid numeric values |
| 4 | Inconsistent categories |
| 5 | Different data formats |

### Verification

The current implementation has been verified through:

| # | Verification Type |
|---|---|
| 1 | Automated testing |
| 2 | Realistic data testing |
| 3 | Performance testing |

> The workflow is **configurable**, tested with realistic datasets, and **optimized for processing larger datasets**.

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Shivanath Samudrala | Initial version — data processing workflow |
