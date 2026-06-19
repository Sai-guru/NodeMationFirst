# Self-Hosted Hybrid AI Agent with Cloud Memory & Vector Retrieval

An advanced, hybrid RAG (Retrieval-Augmented Generation) pipeline built on n8n. This architecture leverages high-performance cloud APIs for reasoning and persistent memory, combined with completely free, self-hosted infrastructure for vector lookups and data processing.

## 🧠 System Architecture

- **Orchestrator:** n8n (Self-Hosted via Docker)
- **LLM Brain:** Groq Chat Model (`openai/gpt-oss-safeguard-20b` via Cloud API)
- **Persistent Chat Memory:** Supabase PostgreSQL (Cloud Database Link)
- **Vector Knowledge Base:** Qdrant Vector Store (Self-Hosted via Docker)
- **Embedding Matrix Model:** Ollama running `llama3.2` (Self-Hosted via Docker)

---

## 🚀 Step-by-Step Deployment Guide

Follow these exact steps to spin up the required local tools and import the workflow canvas.

### Step 1: Spin Up the Local Tools Stack
Instead of building a custom container environment from scratch, we use n8n's official local AI environment stack template to boot the underlying backend services:

```bash
# Clone the official starter infrastructure framework
git clone https://github.com

# Move into the stack folder
cd self-hosted-ai-starter-kit

# Boot up n8n, Qdrant, and Ollama in the background
docker compose up -d
```

### Step 2: Download the Local Embedding Model
Once Docker finishes starting up the containers, pull the exact embedding weights required by the n8n canvas:

```bash
docker exec -it ollama ollama run llama3.2
```
*(Note: If your container name differs based on your environment shell, verify it via `docker ps`)*

### Step 3: Access your Automation Engine
Open your web browser and navigate to your new locally hosted n8n instance dashboard:
👉 **`http://localhost:5678`**

### Step 4: Import the Workflow
1. Open the **`workflow.json`** file included in this GitHub repository.
2. Select and copy the entire raw text block.
3. Go to your fresh n8n dashboard canvas, click anywhere on the empty grid background, and press **`CTRL + V`** (Windows) or **`CMD + V`** (Mac). 
4. The complete AI pipeline structure will instantly appear on your screen!

---

## ⚙️ Mandatary External Credentials Configuration

To wake the agent up, open the newly imported nodes on your canvas and plug in your external connection parameters:

### 1. Groq Chat Model Node
- **Setup:** Create a new credential under `Groq API`.
- **Requirement:** Generate your API key at the [Groq Console](https://groq.com).

### 2. Postgres Chat Memory Node
- **Setup:** Create a new credential under `PostgreSQL`.
- **Requirement:** Go to your **Supabase Dashboard** ➡️ **Project Settings** ➡️ **Database** ➡️ **Connection Info**.
- **Fields Mapping:**
  - **Host:** Copy your Supabase host endpoint.
  - **Port:** `6543` *(Highly recommended: Use the transaction pooler port to maximize performance limits)*
  - **User:** Your Supabase project DB user string.
  - **Database:** `postgres`
  - **SSL:** Toggle this **ON** (Supabase connection parameters strictly enforce SSL).

---

## 🧪 Testing the Pipeline
Once credentials are saved, open the n8n Chat UI window in the bottom corner and submit:
> *"Hey, search the test vector store and tell me what trial data blocks are inside."*

Watch the execution paths flash on your canvas as Groq automatically picks up your custom Qdrant tool description, computes embeddings via Ollama, pulls the vector nodes, and references past interaction records inside Supabase!

## 👤 Author

[**Prigeesh**](https://github.com/Sai-guru)

Arch Linux | n8n | Docker | PostgreSQL | Qdrant Vector Store | Ollama | Groq

Always fell free to discuss...