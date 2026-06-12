
**SCM Assistant Bot**

A Retrieval-Augmented Generation (RAG) chatbot built using Flowise Cloud for answering supplier network and governance-related questions 
using supplier performance data and governance policies.
The chatbot uses:
-  supplier_performance_data.csv
-  SupplyChain_Governance_Policy_v3.2.pdf
to answer supplier-related queries with context-aware and grounded responses.

**Public URL of chatbot:**

 https://cloud.flowiseai.com/chatbot/78db1725-e660-4474-8acd-7cfe6ff949eb


**LLM and Embedding Model Used**

Large Language Model (LLM) - Gemini 2.5 Flash

### Why Gemini 2.5 Flash?

- Fast response generation
- Good reasoning capability
- Better contextual understanding
- Suitable for supplier and governance-based analytical questions
  
### Embedding Model

**gemini-embedding-001**

The embedding model converts uploaded document text into vector representations, allowing the chatbot to perform semantic search instead of exact keyword matching.

This helps the chatbot retrieve relevant information even when the wording of the question differs from the document.

Example:

Query:

```text
problematic suppliers
```

can retrieve:

```text
high risk suppliers
active disruption suppliers
low compliance suppliers
```

### Vector Store

**In-Memory Vector Store**
- Lightweight
- Easy to configure
- Suitable for assignment-scale deployment
- Efficient retrieval for uploaded documents

# Chunk Configurations Tried

Two different chunking configurations were tested to improve retrieval quality.

## Configuration 1

```text
Chunk Size = 1000
Chunk Overlap = 200
```

### Observations
- Better context preservation
- Improved understanding of governance policies
- Reduced chances of splitting important policy information

## Configuration 2

```text
Chunk Size = 500
Chunk Overlap = 100
```

### Observations
- Better retrieval precision
- More accurate for small policy rules
- Worked well for threshold-based queries
- Sometimes lost surrounding context

## Final Configuration Used

```text
Chunk Size = 1000
Chunk Overlap = 200
```
This configuration produced better overall results by preserving more contextual information and improving answer quality for supplier governance and policy-related questions.

# Improvements Made

The following improvements were implemented to improve chatbot performance and retrieval quality.

## 1. Combined Multiple Data Sources

Integrated both:
- `supplier_performance_data.csv`
- `SupplyChain_Governance_Policy_v3.2.pdf`

This allowed the chatbot to combine:
- supplier performance metrics
- governance policies
- risk and disruption rules
for more accurate responses.


## 2. Implemented Retrieval-Augmented Generation (RAG)

Instead of using only an LLM, a RAG architecture was implemented.
This ensured that responses are generated using uploaded supplier documents rather than general model knowledge.
Due to this -
- Reduced hallucinations
- More grounded answers
- Better factual accuracy achieved

---

## 3. Semantic Search Using Embeddings

Used gemini-embedding-001 for semantic retrieval.
This enabled meaning-based search rather than exact keyword matching.

For example:

```text
supplier issues
```
can retrieve relevant information about:

```text
high risk suppliers
low compliance suppliers
disruption flags
```
even if the exact wording is different.

## 4. Chunking Optimization

Tested multiple chunking strategies to improve-
- retrieval quality
- context preservation
- policy understanding
