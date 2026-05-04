# Student Policy Helper 🎓
### RAG-Based Document Question Answering System for UTA Academic Policies

A conversational AI system that allows students to query official University of Texas at Arlington (UTA) policy documents — the Graduate Catalog and Handbook of Operating Policies (HOP) — using natural language questions. Built using a Retrieval-Augmented Generation (RAG) pipeline with local HuggingFace embeddings and FAISS-based semantic search.

---

## 🔍 What It Does

Instead of manually searching through hundreds of pages of UTA policy documents, students can:
- Upload any UTA policy PDF through a simple web interface
- Ask questions in plain English
- Get concise, document-grounded answers with the source chunk visible

---

## 🛠️ Tech Stack

| Component | Tool |
|---|---|
| UI | Streamlit |
| PDF Extraction | pdfplumber |
| Text Chunking | Custom (512 tokens, 50 overlap) |
| Embeddings | HuggingFace (local model) |
| Vector Store | FAISS |
| Answer Generation | LLM via generate.py |
| Version Control | GitHub |

---

## 📁 Project Structure

| File | Description |
|---|---|
| `app.py` | Streamlit web interface — upload PDFs and ask questions |
| `extract.py` | PDF text extraction using pdfplumber |
| `preprocess.py` | Text cleaning and chunking (512 tokens, 50 overlap) |
| `retrieve.py` | FAISS vector store creation and semantic retrieval |
| `generate.py` | Answer generation using LLM |
---

## ⚙️ How to Run

**1. Clone the repository**
```bash
git clone https://github.com/deeksha24dua/student-policy-helper.git
cd student-policy-helper
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Run the app**
```bash
streamlit run app.py
```

**4. Use the app**
- Upload a UTA policy PDF (Graduate Catalog or HOP)
- Click "Process Documents"
- Type your question and get an answer

---

## 🔄 How the Pipeline Works

1. 📁 **PDF Upload** — User uploads a UTA policy PDF via the Streamlit interface
2. 📝 **Text Extraction** — `extract.py` reads the PDF page by page using pdfplumber
3. ✂️ **Chunking** — `preprocess.py` splits text into 512-token chunks with 50-token overlap
4. 🔢 **Embeddings** — HuggingFace model converts each chunk into a semantic vector locally
5. 🗄️ **FAISS Index** — All vectors stored in a FAISS index for fast similarity search
6. 🔍 **Retrieval** — User's question is embedded and top matching chunks are retrieved
7. 💬 **Answer Generation** — `generate.py` sends retrieved chunks + question to LLM → returns a focused answer
   
---

## 📄 Data Sources

- **UTA Graduate Catalog 2025–2026** — Degree requirements, academic policies, regulations
- **UTA Handbook of Operating Policies (HOP)** — University governance and official procedures

---

## 💡 Key Design Decisions

- **Local HuggingFace embeddings** — No OpenAI API key required, runs fully locally
- **512-token chunk size** — Tested against 256 and 1024; 512 preserved complete policy statements best
- **Dynamic chunking with overlap** — 50-token overlap prevents policy statements from being cut at boundaries
- **FAISS for retrieval** — Fast semantic search even across 300+ pages of dense policy text

---

## 👥 Team — Group 10

| Name | Student ID |
|---|---|
| Bhargavi Davanapally | 1002247026 |
| Deeksha Dua | 1002223870 |
| Thanusri Tallapudi | 1002247022 |

University of Texas at Arlington · Data Science · Spring 2026

---

## 📌 Sample Questions You Can Ask

- *"What is the minimum GPA required to graduate?"*
- *"What are the grading policies at UTA?"*
- *"What is DocTract used for?"*
- *"What does the catalog say about academic integrity?"*
- *"What form is used to request a policy change?"*
