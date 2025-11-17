# End-to-End RAG Pipeline with Azure OpenAI and AI Search

This project demonstrates the implementation of a complete Retrieval-Augmented Generation (RAG) pipeline using Python. The architecture is built entirely on the Microsoft Azure cloud ecosystem, leveraging Azure OpenAI for state-of-the-art language models and Azure AI Search for a scalable, high-performance vector database.

The goal of this project is to build an intelligent Q&A system that can answer questions about a specific domain—in this case, wine reviews—by grounding its responses in factual data, thereby overcoming the limitations of static knowledge in standard Large Language Models (LLMs).


## Core Concepts

-   **Retrieval-Augmented Generation (RAG):** An AI framework for improving the quality of LLM responses by grounding the model on external sources of knowledge.
-   **Vector Embeddings:** Numerical representations of text that capture semantic meaning. Similar texts will have similar vectors.
-   **Vector Database:** A specialized database designed to store and query these vector embeddings using high-speed similarity search algorithms (e.g., k-Nearest Neighbors).

## Tech Stack

-   **Cloud Platform:** Microsoft Azure
-   **Language Models:** Azure OpenAI Service (for `text-embedding-ada-002` and `gpt-3.5-turbo`/`gpt-4`)
-   **Vector Database:** Azure AI Search (formerly Cognitive Search)
-   **Orchestration Framework:** LangChain
-   **Programming Language:** Python 3.10+
-   **Core Libraries:** `openai`, `langchain-community`, `langchain-openai`, `azure-search-documents`, `python-dotenv`.

## Setup and Installation

Follow these steps to set up the project environment and run the code.

### 1. Prerequisites

-   An active Azure subscription.
-   An Azure OpenAI resource with deployments for an embedding model (`text-embedding-ada-002`) and a chat model (e.g., `gpt-35-turbo`).
-   An Azure AI Search resource (Free or Basic tier is sufficient).

### 2. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
cd YOUR_REPOSITORY_NAME
```

### 3. Set Up a Virtual Environment

It is highly recommended to use a virtual environment to manage dependencies.

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows
venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate
```

### 4. Install Dependencies

Install all the required Python packages using the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables

The project uses a `.env` file to securely manage API keys and endpoints.

-   Create a new file named `.env` in the root directory of the project.
-   Copy the contents of `.env.example` into your new `.env` file.
-   Fill in the values with your specific credentials from your Azure resources.

```env
# .env file

# Azure OpenAI Credentials
AZURE_OPENAI_ENDPOINT="https://YOUR-AOAI-RESOURCE-NAME.openai.azure.com/"
AZURE_OPENAI_API_KEY="YOUR_AZURE_OPENAI_API_KEY"
AZURE_OPENAI_API_VERSION="2023-07-01-preview"
EMBEDDING_DEPLOYMENT_NAME="your-embedding-deployment-name"
CHAT_DEPLOYMENT_NAME="your-chat-deployment-name"

# Azure AI Search Credentials
SEARCH_SERVICE_NAME="https://YOUR-SEARCH-SERVICE-NAME.search.windows.net"
SEARCH_API_KEY="YOUR_AZURE_SEARCH_ADMIN_KEY"
SEARCH_INDEX_NAME="your-chosen-index-name"
```

## How to Run

Once the setup is complete, you can execute the main script:

```bash
python acs.py
```

The script will perform the full data ingestion and RAG process, printing the final, fact-grounded answer to the console.
