# System Specification: LLM-Driven Development of an AI Regulation RAG Demo for New Zealand

## 1. Project Goal

Develop a highly accessible Retrieval-Augmented Generation (RAG) demo application with pre-loaded document embeddings. Users can ask questions about AI regulation in New Zealand and receive informed answers with source citations, powered by the Tinfoil Inference API. A basic natural language search function leveraging the same embeddings will also be included. An optional light authentication layer may be added. The entire project will be version controlled using GitHub.

## 2. Core Functionality

* **Pre-loaded Embeddings:** The system will utilize pre-existing document embeddings (ideally regenerated using the Nomic Embed text model via Tinfoil).
* **Question Answering with Source Citations:**
    * Users will input natural language questions.
    * The system will embed the query using the Nomic Embed text model via Tinfoil.
    * Relevant document chunks will be retrieved based on similarity with the pre-loaded embeddings.
    * The retrieved chunks will be passed to the chosen LLM on the Tinfoil API (llama 70b, deepseek 70b, or Mistral comparable) to generate an answer.
    * The system should identify which source documents (or chunks) were most relevant to the answer and provide basic citations (e.g., document title or a unique identifier).
* **Natural Language Search:**
    * Users can enter search queries in natural language.
    * The system will embed the search query using the Nomic Embed text model via Tinfoil.
    * The system will retrieve the top N most similar document chunks based on the pre-loaded embeddings.
    * The titles or a snippet of these top documents will be displayed as search results.
* **User Interface:**
    * A Streamlit-based web interface with:
        * A text input area for questions (for the RAG system).
        * A display area for answers with source citations.
        * A separate text input area for natural language search queries.
        * A display area for search results (document titles/snippets).
    * **Optional Light Authentication:**
        * A very lightweight layer for capturing email and captcha, potentially using Supabase.  This feature is optional.  If implemented, it should:
            * Capture an email address using a Streamlit form.
            * Include a simple captcha (e.g., `streamlit-captcha`).
            * Optionally, send a verification email (note: this adds complexity).
            * Use Supabase to store captured email addresses (if this storage method is chosen).
* **Tinfoil API Integration:** All embedding and LLM inference will use the Tinfoil API.
* **Version Control:** The entire codebase will be managed using Git and stored on GitHub.

## 3. Technical Requirements & Considerations

* **Embedding Choice, Storage, and Regeneration:**
    * Regenerate embeddings using the Nomic Embed text model via Tinfoil.
    * Store embeddings in an easily loadable format, with associated metadata for citations.  Options include:
        * ChromaDB
        * FAISS with metadata linking back to document identifiers
        * Supabase vector store
* **Document Chunking and Metadata:**
    * Define a strategy for chunking the original documents.
    * Associate each chunk with metadata for citation (e.g., document title, page number, unique ID).
    * Store this metadata alongside the embeddings.
* **RAG Framework:**
    * Use LangChain or LlamaIndex.
    * The framework must support building a RAG pipeline with citation capabilities (tracking source documents).
* **LLM for Generation:**
    * Choose a suitable model on the Tinfoil API: llama 70b, deepseek 70b, or a comparable model from Mistral.
    * The chosen model should be capable of understanding and referring to provided context for accurate citations.
* **Embedding Model:** Use Nomic Embed text via the Tinfoil API for both document and query embeddings.
* **User Interface Framework:** Streamlit.
* **Optional Light Authentication:** (See details in Core Functionality).
* **Coding Language:** Python.
* **Deployment:** Streamlit Community Cloud.
* **Version Control:** Git and GitHub.

## 4. Claude Code LLM Agent Responsibilities

* **Tinfoil API Integration (Embedding):** Generate code for embedding documents and queries using the Nomic Embed text model.
* **Embedding Management with Metadata:** Implement storage and retrieval of embeddings, along with their associated document metadata for citations.
* **Similarity Search:** Implement efficient similarity search for both question answering and natural language search.
* **RAG Pipeline with Citations:** Develop the RAG pipeline to:
    * Retrieve relevant chunks.
    * Pass them to the LLM on Tinfoil.
    * Identify the source documents used by the LLM.
    * Format and display citations in the answer.
* **Natural Language Search Implementation:** Create functionality to embed search queries and retrieve relevant document titles/snippets.
* **Streamlit UI:** Build the interface with separate sections for:
    * Question answering (with citations).
    * Natural language search.
* **Optional Light Authentication:** If this feature is included, generate code to:
    * Add email input and captcha components in Streamlit.
    * Implement basic email validation.
    * Integrate with Supabase for storing captured emails (if chosen).
* **GitHub Integration:** Assist with initial repository setup and provide guidance on committing code.
* **Deployment Files:** Generate `requirements.txt` and provide deployment instructions for Streamlit Community Cloud.

## 5. Data

* Original AI regulation documents.
* Tinfoil API key.
* Supabase credentials (if optional authentication is used).

## 6. Success Metrics

* **Functional RAG with Citations:** The system answers questions based on the documents and provides clear source citations.
* **Working Natural Language Search:** Users can enter natural language queries and receive relevant document results.
* **Easy Web Access:** The application is accessible via a simple web link.
* **Utilizes Tinfoil API:** The system uses the Tinfoil API for all embedding and generation.
* **Optional Light Authentication:** (If implemented) The basic email/captcha mechanism functions as intended.
* **Version Control:** The project is tracked on GitHub.

## 7. Open Questions and Decisions

* **Document Chunking and Metadata Strategy:** Define a clear strategy for chunking and storing metadata.
* **Citation Mechanism:** How will the system identify and present citations effectively?
* **Specific LLM on Tinfoil:** Finalize the choice of the generation model (llama 70b, deepseek 70b, or Mistral comparable).
* **Embedding Storage:** Decide on the best storage solution for embeddings and metadata (ChromaDB, FAISS + metadata, or Supabase).
* **Implementation of Optional Authentication:** Decide whether to include it and, if so, how to implement it.
