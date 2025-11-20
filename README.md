# 🍷 RAG Implementation with Azure AI Search

This repository contains a complete, end-to-end implementation of a **Retrieval-Augmented Generation (RAG)** system tailored for wine recommendations.

The project is split into two distinct parts: **Data Ingestion** (ETL) and the **Web Application** (API/UI).

## 📂 Project Structure

| Folder | Name | Description |
| :--- | :--- | :--- |
| **`/data_ingestion`** | **The Setup & Loader** | A standalone Python script that reads the raw CSV data, creates embeddings, and uploads them to Azure AI Search. **Run this first.** |
| **`/webapp`** | **The Application** | A FastAPI application containerized with Docker. It connects to the Search Index created by the ingestion script to serve user queries via an API. |

---

## 🏗️ Architecture Overview

1.  **Data Source:** `wine-ratings.csv` (Raw Data).
2.  **Ingestion (ETL):** The script in `/data_ingestion` chunks the data, creates vectors using **Azure OpenAI**, and indexes them in **Azure AI Search**.
3.  **Retrieval:** The `/webapp` queries Azure AI Search to find relevant wines based on user questions.
4.  **Generation:** The `/webapp` sends the retrieved context to **GPT-4** to generate a natural language response.

---

## 🚀 Getting Started

To get this system running, follow these steps in order:

### Step 1: Configure Environment
Both folders require the same Azure credentials. Ensure you have an **Azure OpenAI** resource and an **Azure AI Search** service running.

### Step 2: Ingest Data
Before the app can answer questions, the database must be populated.
1.  Navigate to the `data_ingestion` folder.
2.  Add your `.env` file.
3.  Run the script to index the CSV data.
   ```bash
   cd data_ingestion
   python ingest.py
```
### Step 3: Run the Web App
Once the data is successfully indexed in Azure, you can launch the application to start chatting.

1.  Navigate to the `webapp` folder.
2.  Run locally via Uvicorn.
    ```bash
    cd webapp
    pip install -r requirements.txt
    uvicorn main:app --reload
    ```
3.  Open your browser to `http://localhost:8000/docs` to test the API.

---

## ☁️ Deployment

This repository is configured with a **CI/CD pipeline** using GitHub Actions.

*   **Automated Build:** Every push to `main` builds the Docker image from the `/webapp` directory.
*   **Automated Deploy:** The image is pushed to GitHub Container Registry (GHCR) and automatically deployed to **Azure Container Apps**.

For details on how to configure the GitHub Secrets (`AZURE_CREDENTIALS`, `GHCR_PAT`) required for this pipeline, please see the [Web App README](./webapp/README.md).

---

## 🛠️ Technologies Used

*   **Language:** Python 3.11
*   **Vector Database:** Azure AI Search
*   **LLM & Embeddings:** Azure OpenAI (GPT-4 / Ada-002)
*   **Framework:** FastAPI & LangChain
*   **Containerization:** Docker
*   **Cloud Infrastructure:** Azure Container Apps
*   **CI/CD:** GitHub Actions

---

## 📄 Detailed Documentation

For specific setup instructions, environment variable lists, and usage guides, please refer to the README files located in each sub-folder:

*   👉 **[Data Ingestion (ETL) Documentation](./data_ingestion/README.md)**
    *   *Read this for: Database setup, CSV loading, and vector indexing.*
*   👉 **[Web App & Deployment Documentation](./webapp/README.md)**
    *   *Read this for: API usage, Docker commands, and Azure deployment details.*

## 🤝 Contributing

1.  Fork the repository.
2.  Create a feature branch.
3.  Commit your changes.
4.  Open a Pull Request.
