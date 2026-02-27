# Clinical QA RAG System

Retrieval-Augmented Generation (RAG) system designed to answer clinical guideline questions with high semantic accuracy. By combining the retrieval power of FAISS with the generative capabilities of OpenAI, the system provides precise, context-aware answers based on clinical datasets.

_**Project Overview**_

The system processes clinical data by combining titles and contexts into retrievable knowledge units. It uses a vector-based approach to find relevant information and generate answers that are both deterministic and traceable.

**Key Features:**

- Vector Search: Utilizes FAISS for fast, in-memory similarity searches.
- Semantic Embeddings: Leverages OpenAI text-embedding-ada-002 for high-quality vector representations.
- Interactive Querying: Includes a built-in loop for real-time user questions and answers.
- Advanced Evaluation: Measures performance using BERTScore to ensure semantic similarity between generated answers and ground truth.
- Traceability: Configured to return source documents, allowing users to verify the clinical context used for each answer

**System Architecture:**

- Input: The user submits a clinical question.
- Embedding: The question is converted into a vector using an OpenAI embedding model.
- Retrieval: FAISS identifies and retrieves the most similar data chunks.
- Generation: ChatGPT (gpt-3.5-turbo) generates a final answer using the retrieved context.
- Output: The system delivers a semantically accurate clinical response.

Performance: The system achieves a BERTScore F1 of >92%, demonstrating strong alignment with professional clinical ground truth answers.

**Tech Stack:**
- Framework: LangChain, used to orchestrate the retrieval and generation pipeline.
- Language Model: OpenAI ChatGPT (gpt-3.5-turbo) for generating human-like clinical answers.
- Embeddings: OpenAI text-embedding-ada-002 to create semantic vector representations of text.
- Vector Store: FAISS (Facebook AI Similarity Search) for efficient, in-memory similarity searching
- Evaluation Metric: BERTScore to measure the semantic accuracy and F1 similarity between predicted and ground truth answers.
- Data Handling: Pandas for processing clinical datasets containing titles, contexts, questions, and answers.
- Environment: Google Colab for development and execution.
