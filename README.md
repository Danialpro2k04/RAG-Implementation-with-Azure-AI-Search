# 🍷 Wine Assistant RAG App

A Retrieval-Augmented Generation (RAG) application that acts as an intelligent Wine Assistant. It uses **Azure AI Search** to retrieve wine data and **Azure OpenAI** to generate natural language recommendations.

The app is built with **FastAPI**, containerized with **Docker**, and automatically deployed to **Azure Container Apps** via **GitHub Actions**.

## 🛠️ Tech Stack

*   **Backend:** Python 3.11, FastAPI, Uvicorn
*   **AI & Search:** Azure OpenAI (GPT-3.5/4), Azure AI Search
*   **Infrastructure:** Azure Container Apps, Docker, GitHub Container Registry (GHCR)
*   **CI/CD:** GitHub Actions

## ⚙️ Environment Variables

To run locally or deploy, configure these variables in a `.env` file or Azure settings:

| Variable | Description |
| :--- | :--- |
| `AZURE_OPENAI_ENDPOINT` | URL for Azure OpenAI resource |
| `AZURE_OPENAI_API_KEY` | Azure OpenAI API Key |
| `AZURE_OPENAI_API_VERSION` | e.g., `2023-05-15` |
| `EMBEDDING_DEPLOYMENT_NAME` | e.g., `text-embedding-ada-002` |
| `CHAT_DEPLOYMENT_NAME` | e.g., `gpt-35-turbo` |
| `SEARCH_SERVICE_NAME` | Azure AI Search service name |
| `SEARCH_API_KEY` | Azure AI Search Admin Key |
| `SEARCH_INDEX_NAME` | Name of the search index |

## 💻 Local Setup

1.  **Clone & Install:**
    ```bash
    git clone https://github.com/Danialpro2k04/RAG-Implementation-with-Azure-AI-Search.git
    cd webapp
    python -m venv venv
    source venv/bin/activate  # Windows: venv\Scripts\activate
    pip install -r requirements.txt
    ```

2.  **Run App:**
    ```bash
    uvicorn main:app --host 0.0.0.0 --port 8000 --reload
    ```
    *Swagger UI available at `http://localhost:8000/docs`*

## 🐳 Docker Usage

```bash
docker build -t wine-assistant .
docker run -p 8000:8000 --env-file .env wine-assistant
```

## ☁️ Deployment (CI/CD)

This repo uses **GitHub Actions** to build and deploy to **Azure Container Apps**.

### Architecture
1.  **Build:** Docker image is built and pushed to **GitHub Container Registry (GHCR)**.
2.  **Deploy:** Azure Container App pulls the new image and updates environment variables.
3.  **Ingress:** App listens on port **8000**.

### Required GitHub Secrets
Set these in **Settings > Secrets and variables > Actions**:

*   `AZURE_CREDENTIALS`: JSON output from Azure CLI (`az ad sp create-for-rbac ...`).
*   `GHCR_PAT`: Personal Access Token with `read:packages` scope (used for image pulling).
*   `AZURE_OPENAI_API_KEY`, etc.: All variables listed in the Environment section above.

## 📝 API Example

**POST** `/chat`

```json
{
  "query": "What is a good dry red wine for steak?"
}
