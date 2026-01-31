# NyayaBot
It is a chatbot created to help understand the Indian Constitution with well detailed citations.

## Execution Plan

### Phase 1: Offline Phase
Create a searchable knowledge base of Indian Constitution/Polity content with 
- clean text
- meta data (Article number, Part, Schedule, etc.)
- embedding vector
- stored in Vector DB

#### Step 0: Decide your scope (MVP)
- Constitution Articles only (Part I to XXII)

#### Step 1: Collect the source content
- Original Source: https://www.legislative.gov.in/static/uploads/2025/07/ca7ce5c746fa7480804bbdeb6cb704f0.pdf
- The structered data is stored inside the **__knowledge-base/constitution__** folder

**_Json Like:_**
```json
{
  "articleNumber": 21,
  "title": "Protection of life and personal liberty",
  "part": "Part III",
  "text": "No person shall be deprived..."
}
```

#### Step 2 — Normalize and clean the text

Rules
- remove extra spaces/newlines
- normalize quotes
- remove page headers/footers
- keep clause numbering like: 21A, 21B

#### Step 3: Chunking and enriching

- 1 Article is 1 chunk
- if article is too long split by clause with overlap
- chunk format: 

```json
{
  "articleNumber": 21,
  "title": "Protection of life and personal liberty",
  "part": "Part III",
  "text": "No person shall be deprived...",
  "topics": ["Fundamental Rights", "Right to life with dignity", "Right to privacy", "Right to die with dignity"],
}
```

#### Step 4: Generate embeddings using Ollama
- use __**nomic-embed-text**__ embedding model

#### Step 5: Chunks + Enbeddings store in VectorDB
- Use Qdrant for VectorDB


