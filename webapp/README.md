# 🍷 Wine Assistant Web App

This is the backend API for the Wine Assistant RAG application. It is built with **FastAPI** and uses **LangChain** to orchestrate the retrieval of wine data from **Azure AI Search** and the generation of responses using **Azure OpenAI**.

This application is designed to be containerized with Docker and deployed to **Azure Container Apps**.

---

## 🚀 Features

*   **FastAPI:** High-performance, asynchronous Python web framework.
*   **RAG Architecture:** Retrieves context from vector storage before generating answers.
*   **Swagger UI:** Interactive API documentation available at `/docs`.
*   **Production Ready:** Includes `Dockerfile` for containerized deployment.

---

## ⚙️ Environment Variables

To run this application, you must configure the following environment variables in a `.env` file (locally) or in your Azure Container App settings.

| Variable | Description |
| :--- | :--- |
| `AZURE_OPENAI_ENDPOINT` | The endpoint URL for your Azure OpenAI resource. |
| `AZURE_OPENAI_API_KEY` | Your Azure OpenAI API key. |
| `AZURE_OPENAI_API_VERSION` | API version (e.g., `2023-05-15`). |
| `EMBEDDING_DEPLOYMENT_NAME` | Name of your embedding model deployment (e.g., `text-embedding-ada-002`). |
| `CHAT_DEPLOYMENT_NAME` | Name of your chat model deployment (e.g., `gpt-35-turbo` or `gpt-4`). |
| `SEARCH_SERVICE_NAME` | The name of your Azure AI Search service. |
| `SEARCH_API_KEY` | The admin key for your Search service. |
| `SEARCH_INDEX_NAME` | The name of the index containing your wine data. |

---

## 💻 Local Development Setup

1.  **Navigate to the directory:**
    ```bash
    cd webapp
    ```

2.  **Create and activate virtual environment:**
    ```bash
    python -m venv venv
    # Windows:
    venv\Scripts\activate
    # Mac/Linux:
    source venv/bin/activate
    ```

3.  **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the Application:**
    The app runs on port **8000**.
    ```bash
    uvicorn main:app --host 0.0.0.0 --port 8000 --reload
    ```

5.  **Test the API:**
    Open your browser to `http://localhost:8000/docs`.

---

## 🐳 Docker Setup

You can build and run the image locally to simulate the production environment.

```bash
# Build the image
docker build -t wine-assistant .

# Run the container (ensure you have a .env file)
docker run -p 8000:8000 --env-file .env wine-assistant
```
## ☁️ Azure Deployment (CI/CD)

This folder is deployed automatically via the **GitHub Actions** workflow located in `.github/workflows/main.yml`.

### Workflow Summary
1.  **Build:** Docker image is built and pushed to **GitHub Container Registry (GHCR)**.
2.  **Deploy:** Azure CLI updates the **Azure Container App** with the new image.

### Configuration Requirements
For the deployment to succeed, your Azure Container App must be configured with:

1.  **Ingress Target Port:** Set to **8000** (Since Uvicorn listens on 8000).
2.  **Secrets:** The GitHub repository requires the following secrets:
    *   **`AZURE_CREDENTIALS`**: The JSON output from the Azure CLI service principal creation.
    *   **`GHCR_PAT`**: A GitHub Personal Access Token with `read:packages` scope (used by Azure to pull the image).
    *   *Plus all the Environment Variables listed in the table above.*

---

## 📝 API Example

**Endpoint:** `POST /chat`

**Request:**
```json
{
  "query": "What is a good dry red wine for steak?"
}
