# Enterprise RAG + Text-to-SQL Chatbot

## Project Overview
The project is a robust, privacy-first **Enterprise Knowledge-Based Chatbot** backend built on **FastAPI**. It leverages local Large Language Models (LLMs) via **Ollama**, ensuring sensitive company data never leaves the internal network. The system combines Retrieval-Augmented Generation (RAG) for unstructured documents with Text-to-SQL capabilities for structured tabular data. 

## Key Features & Updates

### 1. Advanced Document Processing (RAG)
*   **Upgraded PDF Extraction pipeline:** The project recently moved away from basic OCR fallbacks and integrated **Docuforge** alongside the **Adobe PDF Extract API**. This provides a vastly superior structural understanding of complex documents (perfectly detecting tables, headers, nested lists, and reading order), which drastically improves the quality of the chunks passed to the LLM. 
*   **Vector Database:** Uses **ChromaDB** to store and query document embeddings locally using the `nomic-embed-text` model.

### 2. Text-to-SQL for Tabular Data
*   Allows users to upload tabular data (CSV/Excel) which is ingested into a local SQLite database. The LLM can then seamlessly generate and execute SQL queries to answer questions about the structured data.

### 3. New Reporting & Export Engine
*   The system now includes a dedicated reporting module that can compile the LLM's structured insights and output them directly into downloadable **PDFs**, **Word Documents (.docx)**, and **Markdown**. *(This is the feature that required adding `markdown` and `xhtml2pdf` to the dependencies!)*

### 4. Hybrid Chat & Web Search Fallback
*   The chatbot follows a "fallback chain": it first attempts to answer questions using internal uploaded documents. If the answer isn't found, it falls back to a free, API-key-less web search (via DuckDuckGo), and finally to the LLM's general knowledge.
*   It utilizes robust LLM models like `gpt-oss:20b-cloud` for generation and `gemma4:cloud` for vision-based OCR tasks on scanned PDFs.

### 5. Enterprise Security & Management
*   **Authentication:** Fully implemented JWT-based user authentication and role-based access control (Admin vs. Regular Users).
*   **Audit Logging:** Tracks user queries, system actions, and rate limits usage per user (e.g., 20 requests/min).
*   **Cloud Syncing (Optional):** Includes optional integrations with Supabase to mirror audit logs and user feedback for external dashboards.

In short, it is a highly capable, self-hosted AI engine designed to safely extract, analyze, query, and generate reports from complex enterprise documents and spreadsheets!
