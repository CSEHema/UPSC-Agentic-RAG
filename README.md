# UPSC-Agentic-RAG: Specialized Subject-Matter Expert System

An advanced **Agentic Retrieval-Augmented Generation (RAG)** pipeline designed for UPSC CSE preparation. The system processes a 142-PDF syllabus and routes queries to subject-specific "expert" vector databases to eliminate cross-domain hallucinations and improve factual accuracy.

## 🚀 Technical Architecture

The system utilizes a **ReAct Agent** architecture to decide the optimal retrieval path for a given query:

$$\text{Query} \rightarrow \text{Agent Router} \rightarrow \begin{cases} \text{History Expert DB} \\ \text{Polity Expert DB} \\ \text{Geography Expert DB} \\ \text{Economics Expert DB} \end{cases} \rightarrow \text{Structured Response}$$

### Key Components
- **Brain:** Groq LPU™ Inference Engine (using `llama-3.1-8b-instant`).
- **Vector Store:** ChromaDB with Subject-level isolation.
- **Embeddings:** `BAAI/bge-small-en-v1.5` (running locally).
- **Orchestration:** LangGraph for the Agentic loop and state management.

## 🛠️ Data Pipeline

The ingestion pipeline transforms raw PDFs into specialized expert databases:

1. **Preprocessing:** Recursive character splitting with a chunk size of $1000$ and overlap of $200$.
2. **Metadata Tagging:** Captures source file names and subject categories from folder structures.
3. **Vectorization:** Generates normalized embeddings for high-dimensional similarity search.

## 📊 Evaluation Results

Performance was validated using a **LLM-as-a-Judge** framework and a "Mini-Benchmark" across core subjects.

| Topic | Status | 
| :--- | :--- |
| Socialism in Europe & Russian Revolution | ✅ Success |
| Nazism and the Rise of Hitler | ✅ Success |
| Physical Features of India | ✅ Success |
| Drainage Systems | ✅ Success |
| Minerals and Energy Resources | ✅ Success |

## ⚙️ Installation

```bash
# Install dependencies
pip install -r requirements.txt

# Initialize the environment
python -m venv venv
source venv/bin/activate  # Windows: .\venv\Scripts\activate
