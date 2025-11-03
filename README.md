#  Semantic Search with FAISS and Sentence Transformers

This project demonstrates how to build a **semantic search engine** using **FAISS**, **Sentence Transformers**, and **Python**.  
It enables you to upload `.pdf`, `.docx`, or `.txt` files, extract their content, create embeddings, and perform **semantic similarity search** across documents.

---

##  Overview

The goal of this project is to search across multiple documents and retrieve the most relevant text sections **based on meaning**, not just keyword matches.  
It uses **Sentence Transformers** for embeddings and **FAISS** for efficient similarity search.

---

##  Features

-  Extracts text from **PDF**, **Word**, and **Text** files  
-  Automatically splits text into smaller chunks for embeddings  
-  Generates embeddings using `all-MiniLM-L6-v2` model  
-  Builds a **FAISS vector index** for fast search  
-  Performs **semantic search** with similarity scoring  
-  Cleans and formats search results for easy reading  

---

##  Project Structure

```plaintext
├── extract_text_from_file()     # Extracts text from PDFs, DOCX, and TXT files
├── chunk_text()                 # Splits text into smaller chunks for embedding
├── generate_embeddings()        # Creates dense vector embeddings for text
├── build_faiss_index()          # Builds and stores FAISS index
├── semantic_search_best()       # Performs semantic search on the index
└── main.ipynb                   # Main notebook combining all steps
```
---

##  Installation

Install the required libraries before running the notebooks:

```bash
pip install faiss-cpu sentence-transformers python-docx PyMuPDF PyPDF2 numpy
```
---

#  Dependencies

| Library | Purpose |
|----------|----------|
| **faiss-cpu** | Fast similarity search and clustering of dense vectors |
| **sentence-transformers** | Creates text embeddings |
| **python-docx** | Reads `.docx` files |
| **PyMuPDF** | Extracts text from PDF files |
| **PyPDF2** | Alternative library for PDF reading |
| **numpy** | Array and vector operations |
| **re, textwrap** | Text cleaning and formatting |

---

#  How It Works

### 1. Document Extraction
Reads files (`.pdf`, `.docx`, `.txt`) from a folder and extracts text using:

- **PdfReader** for PDFs  
- **Document** from `python-docx` for Word files  
- **open()** for plain text files  

---

### 2. Text Chunking
Splits extracted text into smaller chunks (default: ~300 words per chunk).  
Each chunk becomes a separate searchable unit.

---

### 3. Embedding Generation

```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer('all-MiniLM-L6-v2')
faiss.normalize_L2()
Converts each chunk into a 384-dimensional embedding and normalizes it using FAISS.
```
### 4. FAISS Indexing
Builds a FAISS Inner Product index for similarity-based search and stores all embeddings.

### 5. Semantic Search
Encodes a user query, searches the index for the most similar text chunks, and returns ranked results with similarity scores.

# Example Output
```bash
Top Semantic Search Result(s):
========================================================================================================================
Rank 1
Source File     : ai_intro.pdf
Similarity Score: 0.5430
------------------------------------------------------------------------------------------------------------------------
Preview Snippet:
Artificial Intelligence (AI) Introduction Artificial Intelligence refers to the simulation of human
intelligence in machines that are programmed to think and act like humans...
========================================================================================================================
```
---
#  Example Folder Structure
```bash
/content
 ├── ai_intro.pdf
 ├── data_science.docx
 └── db_basics.txt
```
# Author
Anurag Tripathi
