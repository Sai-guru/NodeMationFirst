# Self-Hosted AI Agent with Vector Memory (RAG Pipeline)

An end-to-end Retrieval-Augmented Generation (RAG) pipeline built using n8n, Groq, Ollama, and Qdrant. 

## 🚀 Architecture
- **Orchestration:** n8n (Self-Hosted)
- **LLM Brain:** Groq Chat Model (Ultra-fast execution)
- **Embeddings:** Local Ollama Server
- **Vector Store:** Qdrant (Handles semantic chunk retrieval)

## 📦 How to Use This Workflow
1. Create a new, blank workflow in your n8n instance.
2. Open the `workflow.json` file from this repository and copy the entire text content.
3. Click anywhere on your n8n canvas and press `CMD+V` (Mac) or `CTRL+V` (Windows) to paste the entire node structure instantly.

## ⚙️ Configuration Notes
- **Ollama URL:** If running n8n via Docker, ensure your Ollama connection URL is set to `http://docker.internal` so n8n can route outside its container to hit your local desktop Ollama instance.
- **Qdrant URL:** Use `http://docker.internal` for your local Qdrant container endpoint.
- Ensure you set a descriptive string in the Qdrant Tool Node so the LLM agent understands when to execute the vector search.
