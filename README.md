# 🚀 Space Exploration Multi-Query RAG

A Retrieval-Augmented Generation (RAG) system built using Python, Pinecone, Sentence Transformers, Hugging Face Transformers, and Qwen.

This project uses a Space Exploration document as the knowledge source and implements Vanilla RAG, Multi-Query Generation, Pinecone Multi-Tenancy, and Reranking to provide relevant answers to user questions.

---

## 📌 Project Overview

The system allows users to ask questions about Space Exploration.

Instead of searching Pinecone using only the original question, the system generates five semantically similar questions. These questions are used to retrieve relevant information from Pinecone.

The retrieved results are then reranked to identify the most relevant context, which is finally passed to the language model to generate the final answer.

---

## 🏗️ Architecture

```text
                         User Question
                              │
                              ▼
                    Multi-Query Generation
                              │
                              ▼
                  5 Similar Questions
                              │
                              ▼
                     Pinecone Retrieval
                              │
                              ▼
                    Relevant Document Chunks
                              │
                              ▼
                         Reranking
                              │
                              ▼
                    Best Relevant Context
                              │
                              ▼
                          Qwen LLM
                              │
                              ▼
                       Final Answer
```

---

## ✨ Features

### 1. Vanilla RAG

The Space Exploration document is loaded, split into chunks, converted into embeddings, stored in Pinecone, and retrieved based on user queries.

### 2. Multi-Query Generation

For a single user question, the system generates five semantically similar questions.

Example:

**Original Question:**

> Which rocket is the most powerful?

**Generated Questions:**

1. What is the most powerful rocket?
2. Which rocket has the highest thrust?
3. What is the strongest rocket?
4. Which rocket is considered the most powerful?
5. What rocket has the greatest thrust?

These questions improve the chances of retrieving relevant information.

### 3. Pinecone Multi-Tenancy

The project demonstrates a **one-to-many architecture**:

```text
One Space Exploration Document
              │
              ▼
           Pinecone
              │
       ┌──────┼──────┐
       ▼      ▼      ▼
     User 1 User 2 User 3
```

The same Space Exploration knowledge base can be accessed by multiple users. Each user can submit their own question while using the same document.

Pinecone namespaces are used to represent individual users/tenants.

### 4. Reranking

The retrieved results from the multiple queries are passed through a reranking model. The reranker compares the original question with retrieved document chunks and assigns relevance scores. The highest-ranked result is selected as the best context.

### 5. Final Answer Generation

The best-ranked context is passed to the Qwen language model. The model generates a short and direct answer to the user's original question.

The five similar questions are used internally and do not need to be shown to the end user.

---

## 📚 Knowledge Source

The project uses a Space Exploration document containing information about:

- Rockets
- Saturn V
- Escape Velocity
- Low Earth Orbit (LEO)
- International Space Station
- Apollo 11
- Moon missions

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Google Colab | Development environment |
| Sentence Transformers | Text embeddings |
| Pinecone | Vector database and retrieval |
| Hugging Face Transformers | LLM and reranking |
| Qwen | Answer generation |
| LangChain | Document processing |
| PyPDF | PDF processing |

---

## 📦 Installation

Clone the repository:

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd Space-Exploration-RAG
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

---

## 🔑 API Keys

Do not hard-code API keys in the notebook or upload them to GitHub.

Set required credentials using environment variables.

Example:

```python
import os

os.environ["OPENAI_API_KEY"] = os.getenv("OPENAI_API_KEY")
os.environ["PINECONE_API_KEY"] = os.getenv("PINECONE_API_KEY")
```

Never commit real API keys to the repository.

---

## ▶️ How to Run

1. Open `Space_Exploration_RAG.ipynb`.
2. Install the required dependencies.
3. Configure the required API keys.
4. Load the Space Exploration document.
5. Split the document into chunks.
6. Generate embeddings.
7. Upload vectors to Pinecone.
8. Run Multi-Query Generation.
9. Perform Pinecone retrieval.
10. Apply reranking.
11. Generate the final answer.

---

## 💡 Example

### Input

```text
Which rocket is the most powerful?
```

### Processing

```text
Original Question
       ↓
5 Similar Questions
       ↓
Pinecone Retrieval
       ↓
Reranking
       ↓
Best Context
       ↓
Qwen
```

### Output

```text
The Saturn V rocket was the most powerful rocket ever successfully flown,
generating 7.5 million pounds of thrust at liftoff.
```

---

## 📁 Project Structure

```text
Space-Exploration-RAG/
│
├── Space_Exploration_RAG.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 🔄 Complete Workflow

```text
Space Exploration Document
            ↓
       Text Chunking
            ↓
        Embeddings
            ↓
         Pinecone
            ↓
      User Question
            ↓
   Multi-Query Generation
            ↓
    5 Similar Questions
            ↓
   Pinecone Vector Search
            ↓
    Retrieved Chunks
            ↓
        Reranking
            ↓
   Best Relevant Context
            ↓
         Qwen LLM
            ↓
       Final Answer
```

---

## 🎯 Project Objectives

- Implement a basic Vanilla RAG pipeline.
- Improve retrieval using Multi-Query Generation.
- Implement Pinecone vector search.
- Demonstrate one-to-many multi-tenancy.
- Improve retrieval quality using reranking.
- Generate concise answers using an LLM.

---