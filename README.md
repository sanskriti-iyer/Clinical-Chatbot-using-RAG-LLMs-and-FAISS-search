# Clinical Guidelines RAG Chatbot

A Retrieval-Augmented Generation (RAG) chatbot built to answer clinical questions based on the VA/DoD Clinical Practice Guidelines for Opioid Therapy for Chronic Pain.

## Overview

This project implements a RAG pipeline that retrieves relevant chunks from a clinical guidelines PDF and generates accurate, context-grounded answers to user queries. The system cites page numbers from the source document in its responses.

## Data Source

VA/DoD Clinical Practice Guideline for Opioid Therapy for Chronic Pain
https://www.healthquality.va.gov/HEALTHQUALITY/guidelines/Pain/cot/VADODOpioidsCPG.pdf

## Tech Stack

- **LLM**: Llama 3.3 70B via Groq API
- **Embeddings**: all-MiniLM-L6-v2 (sentence-transformers)
- **Vector Store**: Chroma
- **Framework**: LangChain
- **PDF Loader**: PyPDFLoader
- **Evaluation**: BERTScore, ROUGE

## Pipeline

1. Load and chunk the VA/DoD opioid guidelines PDF using PyPDFLoader and RecursiveCharacterTextSplitter
2. Embed chunks using all-MiniLM-L6-v2 and store in Chroma vector store
3. Retrieve top 3 relevant chunks for each user query
4. Generate answers using Llama 3.3 70B with source page citations
5. Evaluate generated answers against ground truth using BERTScore and ROUGE

## Evaluation Results

| Metric | Score |
|--------|-------|
| BERTScore Precision | 0.81 |
| BERTScore Recall | 0.83 |
| BERTScore F1 | 0.82 |
| ROUGE-1 | 0.06 |
| ROUGE-L | 0.04 |

ROUGE scores are low due to paraphrasing rather than incorrect answers. BERTScore is the more meaningful metric here as it measures semantic similarity.

## Setup

1. Clone the repository
2. Create a conda environment with Python 3.10
3. Install dependencies: `pip install -r requirements.txt`
4. Add your Groq API key to a `.env` file: `GROQ_API_KEY=your_key_here`
5. Run the notebook

## Dataset

Evaluation was performed using the cpgQA-v1.0 dataset, which contains question-answer pairs derived from the same VA/DoD opioid clinical practice guidelines PDF used as the knowledge base.

## Limitations

- Runs on CPU only, no GPU required
- Groq free tier rate limits may slow down batch evaluation
- flan-t5 was tested but replaced with Llama 3.3 70B via Groq for better instruction following
