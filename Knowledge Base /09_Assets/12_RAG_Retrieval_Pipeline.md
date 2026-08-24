## 12. RAG Retrieval Pipeline

```mermaid
flowchart LR
    A[User Query] --> B[Query Preprocessing]
    B --> C[Query Embedding]
    C --> D[FAISS Similarity Search]
    D --> E[Candidate Chunks]
    E --> F[Top-K Retrieval]
    F --> G[Relevant Context]
    G --> H[Prompt Construction]
    H --> I[Llama 3.1 / Ollama]
    I --> J[Final Answer]
```
