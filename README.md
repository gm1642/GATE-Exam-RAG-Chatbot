# GATE Exam Chatbot: RAG-Powered Study Assistant

[![Stack](https://img.shields.io/badge/Stack-Next.js%20%7C%20FastAPI-black)]()
[![Model](https://img.shields.io/badge/LLM-Llama3%3A8B-blue)](https://ollama.com/)
[![Database](https://img.shields.io/badge/Vector%20DB-Weaviate-green)](https://weaviate.io/)
[![Deployment](https://img.shields.io/badge/Docker-Container-blue?logo=docker)](https://www.docker.com/)

A high-performance **Retrieval-Augmented Generation (RAG)** chatbot designed to help students prepare for the **GATE (Graduate Aptitude Test in Engineering)**. It retrieves exact solutions from past exam papers and uses **Llama-3-8B** to provide intelligent, context-aware explanations and follow-up answers.

## 🏗️ System Architecture
The system follows a microservices architecture fully containerized with **Docker**.
![System Architecture](assets/architecture_v0.2.png)
*Figure 1: v0.2 Architecture - integrating Mathpix OCR, Weaviate Vector DB, and Llama-3 generation.*

### Key Components
1.  **Data Pipeline:**
    * **OCR:** Used **Mathpix** to extract complex mathematical equations (LaTeX) from PDF exam papers.
    * **Chunking:** Semantic chunking strategies to preserve context.
    * **Embedding:** **BGE-Small-EN-v1.5** selected for superior performance on mathematical datasets.
2.  **RAG Engine:**
    * **Vector Store:** **Weaviate** (Self-hosted via Docker).
    * **LLM:** **Llama3:8B-instruct-q2_K** (Quantized) running via **Ollama** for low-latency local inference.
3.  **User Interface:**
    * **Frontend:** **Next.js** with JWT authentication. Features a searchable dropdown for questions.
    * **Backend:** **FastAPI** handling asynchronous requests and MongoDB session storage.

## 🚀 Features (v0.2)
* **Exact Solution Retrieval:** Fetches the verified solution from the database to ensure 100% accuracy.
* **AI Explanations:** Users can ask follow-up questions ("Why is option B wrong?"), and Llama-3 explains using the retrieved context.
* **Smart Search:** Dropdown filter to find questions by Year (e.g., 2023) or Domain.
* **AI Notes:** Automatically summarizes study sessions into concise notes.

## 📊 Benchmarks & Evaluation
We conducted extensive benchmarking to select the optimal model configuration.

| LLM Model | Embedding Model | Faithfulness | Answer Relevance |
| :--- | :--- | :--- | :--- |
| **Llama-3:8B (Quantized)** | **BGE-Small** | **0.94** | **0.83** |
| Phi-3 | BGE-Small | 0.87 | 0.78 |
| GPT-3.5-turbo | N/A | 0.56 | 0.49 |

*Table 1: Evaluation results showing Llama-3's superior context adherence.*

## 🛠️ Setup & Installation
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/GATE-RAG-Chatbot.git](https://github.com/your-username/GATE-RAG-Chatbot.git)
    cd GATE-RAG-Chatbot
    ```
2.  **Start Services (Docker):**
    ```bash
    docker-compose up -d
    ```
    *This spins up Weaviate, MongoDB, and the FastAPI backend containers.*
3.  **Run Frontend:**
    ```bash
    cd frontend
    npm install && npm run dev
    ```

## 📸 Demo
![Chatbot Demo](assets/demo_ui.png)
*Figure 2: The student dashboard showing exact retrieval and AI follow-up.*

---
*Developed Summer 2024 as part of the Amulate Research Mentorship.*