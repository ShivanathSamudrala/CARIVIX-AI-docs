---
title: "Model Workflow"
document_id: "ML-03"
version: "1.0"
status: "Final"
last_updated: "2026-09-18"
Author: Shivanath Samudrala
Role: Technical Writer
---

# Model Workflow

## 1. Model Workflow Overview

The model workflow defines how a user request moves through the CARIVIX AI system until the required prediction or result is generated.

### Overall Flow

```text
User Query
    → NLP Processing
    → Intent Detection
    → Entity / Feature Extraction
    → Domain Mapping
    → Input Validation
    → Model Service
    → Trained Model
    → Inference
    → Prediction
    → Response Generation
    → Final CARIVIX Output
```

### Main Stages

| # | Stage |
|---|---|
| 1 | User query handling |
| 2 | NLP processing |
| 3 | Intent detection |
| 4 | Entity / feature extraction |
| 5 | Domain mapping |
| 6 | Input validation |
| 7 | Model inference |
| 8 | Prediction generation |
| 9 | Response generation |
| 10 | Final CARIVIX output |

---

## 2. User Query and Input Handling

The workflow starts when the user provides a natural-language query to CARIVIX.

**Example:**

> "Show me the predicted value for this business based on the available features."

The system receives the query through the application/API layer.

**Input handling includes:**

- Receiving the user query
- Validating the request
- Identifying the requested operation
- Passing the query to the NLP layer
- Maintaining the required request structure

---

## 3. NLP Processing and Intent Detection

The NLP layer converts the natural-language query into structured information that the ML system can understand. The system identifies the intent of the query.

**Example:**

| Field | Value |
|---|---|
| User Query | "Predict the business performance for this location" |
| Intent | `business_prediction` |

The intent classifier determines which operation should be performed.

**Responsibilities:**

- Text normalization
- Tokenization / preprocessing
- Intent classification
- Query classification
- Identification of prediction-related requests
- Routing the request to the appropriate workflow

The CARIVIX intent-classification pipeline can use the configured ML/NLP classification approach to determine the required operation.

---

## 4. Entity and Feature Extraction

After identifying the intent, the system extracts the information required by the ML model.

**Example:**

| Field | Value |
|---|---|
| Query | "Predict business performance for a location with high population and good accessibility" |
| Extracted Information | Population, Accessibility, Location, Business-related attributes |

This stage converts natural language into structured model features.

**Main functions:**

- Entity extraction
- Attribute extraction
- Feature identification
- Value extraction
- Feature-name normalization
- Missing-value identification

The output should be **structured information** rather than raw text.

---

## 5. Domain Mapping and Feature Preparation

The extracted natural-language information is mapped to the exact features expected by the trained ML model.

**Example mapping:**

```text
Natural Language
    ↓
"High population"
    ↓
population = required numeric value
```

**The system performs:**

- Domain-specific feature mapping
- Feature-name matching
- Value normalization
- Data-type conversion
- Required-field checking
- Feature ordering
- Input schema validation

The final structure should match the **model's expected input**.

---

## 6. Model Input Validation

Before sending data to the trained model, the Model Service validates the input. This prevents incorrect or incomplete data from reaching the inference stage.

**Validation includes:**

- Required feature verification
- Data-type validation
- Numeric-range validation
- Missing-value checking
- Feature-order validation
- Schema validation
- Preprocessing consistency

**Example — Model Expected Input:**

```json
[
  "feature_1",
  "feature_2",
  "feature_3",
  "feature_4"
]
```

The Model Service ensures that the received input follows the **same structure used during model training**.

---

## 7. Model Service and Trained ML Model

The validated input is passed to the **Model Service**, which acts as the interface between the CARIVIX AI system and the trained ML model.

**The Model Service is responsible for:**

- Loading the trained model
- Managing model configuration
- Accepting structured input
- Performing inference
- Returning predictions
- Handling model errors
- Maintaining a consistent prediction interface

The trained model may be provided by the Data Science / ML pipeline as a model artifact such as a `.pkl` file.

---

## 8. Model Inference and Prediction

The trained ML model performs the actual prediction using the prepared features.

**Basic process:**

```text
Input Features
    ↓
Preprocessing
    ↓
Trained Model
    ↓
Inference
    ↓
Prediction
```

**Example prediction output:**

```json
{
  "prediction": 0.82
}
```

The inference layer should ensure:

- Correct model version
- Correct preprocessing
- Correct feature order
- Correct input dimensions
- Consistent prediction format

The model output is then passed back to the AI / application layer.

---

## 9. Prediction Response and CARIVIX Integration

The raw ML prediction is transformed into a useful response for the CARIVIX application.

**The response layer can:**

- Format the prediction
- Add relevant explanation
- Combine model output with retrieved information when required
- Return structured JSON / API responses
- Provide user-readable results
- Send results to downstream GIS / visualization components when applicable

This allows the technical ML output to become a meaningful CARIVIX result.

---

## 10. Conclusion

The CARIVIX Model Workflow provides an end-to-end path from a natural-language user query to a final ML prediction.

### Complete Workflow

```text
Natural Language Query
        ↓
NLP Processing
        ↓
Intent Detection
        ↓
Entity / Feature Extraction
        ↓
Domain Mapping
        ↓
Input Validation
        ↓
Model Service
        ↓
Trained Model → Inference → Prediction
        ↓
Response Generation
        ↓
Final CARIVIX Output
```

### Key Outcomes

| Outcome | Description |
|---|---|
| Natural-language input | Converted into structured model features |
| Model Service | Provides a controlled interface to the trained ML model |
| Trained model | Performs inference using validated inputs |
| Prediction | Transformed into a user-understandable response |
| Final result | Can be integrated with the broader CARIVIX AI, NLP, and GIS architecture |

---

## Version Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 2026-09-18 | Nerella Raghavendra Guptha | Initial version — Model workflow documentation |
