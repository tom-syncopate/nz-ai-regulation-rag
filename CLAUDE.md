# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an AI Regulation RAG (Retrieval-Augmented Generation) demo application for New Zealand. The application allows users to ask questions about AI regulation in New Zealand and receive informed answers with source citations, powered by the Tinfoil Inference API. It also includes a natural language search function leveraging document embeddings.

## Technology Stack

- **Language**: Python
- **Framework**: Streamlit for UI
- **RAG Framework**: LangChain or LlamaIndex
- **Embedding Model**: Nomic Embed text via Tinfoil API
- **LLM**: Tinfoil API (llama 70b, deepseek 70b, or Mistral comparable)
- **Vector Database**: ChromaDB, FAISS, or Supabase vector store
- **Optional Authentication**: Streamlit forms with Supabase
- **Deployment**: Streamlit Community Cloud
- **Version Control**: Git and GitHub

## Core Components

1. **Embedding System**: 
   - Pre-loaded document embeddings using Nomic Embed text model via Tinfoil
   - Document chunking with associated metadata for citations

2. **Question Answering Pipeline**:
   - Embed user queries using Nomic Embed text model
   - Retrieve relevant document chunks based on similarity
   - Generate answers using Tinfoil API LLM
   - Provide source citations

3. **Natural Language Search**:
   - Embed search queries using Nomic Embed text model
   - Retrieve top N most similar document chunks
   - Display titles or snippets as search results

4. **User Interface**:
   - Text input for questions
   - Display area for answers with citations
   - Text input for search queries
   - Display area for search results

5. **Optional Authentication**:
   - Email capture with captcha
   - Supabase for storing emails

## Common Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run the Streamlit application locally
streamlit run app.py

# Run tests
pytest

# Lint code
flake8 .
```

## Environment Variables

- `TINFOIL_API_KEY`: API key for Tinfoil
- `SUPABASE_URL`: Supabase URL (if using authentication)
- `SUPABASE_KEY`: Supabase key (if using authentication)

## Data Management

- Original AI regulation documents are chunked and embedded
- Embeddings are stored with metadata for citations
- Similarity search is used for both question answering and natural language search