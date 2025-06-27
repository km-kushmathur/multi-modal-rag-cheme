# Multi-modal RAG for Chemical Engineering

This repository contains the code and resources to build a multi-modal Retrieval-Augmented Generation (RAG) system tailored for chemical engineering content. The system can ingest a PDF textbook and answer questions about its text, tables, and even the content within its images and diagrams.

## Features

* **Multi-modal Ingestion**: Processes text, tables, and images from PDF documents using `unstructured.io`.
* **Advanced Retrieval**: Employs a `MultiVectorRetriever` strategy, searching over concise summaries of content for higher accuracy.
* **Hybrid LLM Approach**: Uses fast, open-source models (via Groq) for text summarization and powerful multi-modal models (like GPT-4o) for image analysis.
* **Reproducible Environment**: Includes a `requirements.txt` and clear setup instructions for easy replication.

## Repository Structure

```
multi-modal-rag-cheme/
│
├── .gitignore
├── content/
│   └── YOUR_PDF_FILE.pdf
├── RAG_Notebook.ipynb
├── LICENSE
├── README.md
└── requirements.txt
```

## Setup and Installation

Follow these steps to set up the project environment. This system is designed to run in a Linux environment (WSL on Windows is recommended).

### 1. System-Level Dependencies

First, install the necessary libraries for PDF and image processing. On a Debian/Ubuntu-based system, run:

```bash
sudo apt-get update && sudo apt-get install -y poppler-utils tesseract-ocr libmagic-dev
```

### 2. Clone the Repository

```bash
git clone https://github.com/KushMathur/multi-modal-rag-cheme.git
cd multi-modal-rag-cheme
```

### 3. Create and Activate a Python Virtual Environment

```bash
# Create the virtual environment
python3 -m venv venv

# Activate the environment
source ./venv/bin/activate
```

### 4. Install Python Dependencies

All required Python packages are listed in `requirements.txt`.

```bash
pip install -r requirements.txt
```

### 5. Configure API Keys

Create a file named `.env` in the root of the project folder. You can do this with the command `touch .env`. Then, open the file and paste the following content into it, replacing the placeholders with your secret API keys.

```
# Azure OpenAI - Multi-modal LLM (for generation and image summaries)
OPENAI_API_TYPE="azure"
AZURE_OPENAI_ENDPOINT="YOUR_MULTIMODAL_LLM_ENDPOINT"
OPENAI_API_VERSION="YOUR_MULTIMODAL_LLM_API_VERSION"
AZURE_OPENAI_API_KEY="YOUR_MULTIMODAL_LLM_API_KEY"
AZURE_OPENAI_DEPLOYMENT_NAME="YOUR_MULTIMODAL_LLM_DEPLOYMENT_NAME"

# Azure OpenAI - Embedding Model
AZURE_EMBEDDING_ENDPOINT="YOUR_EMBEDDING_MODEL_ENDPOINT"
AZURE_EMBEDDING_API_KEY="YOUR_EMBEDDING_MODEL_API_KEY"
AZURE_EMBEDDING_DEPLOYMENT_NAME="YOUR_EMBEDDING_MODEL_DEPLOYMENT_NAME"
EMBEDDING_API_VERSION="YOUR_EMBEDDING_MODEL_API_VERSION"

# Groq API (for fast text summarization)
GROQ_API_KEY="YOUR_GROQ_API_KEY"

# LangChain API (for tracing/debugging, optional)
LANGCHAIN_API_KEY="YOUR_LANGCHAIN_API_KEY"
LANGCHAIN_TRACING_V2="false"
```

## How to Run in VS Code

1.  **Place Your PDF**: Add the PDF file you want to process into the `content/` directory.
2.  **Open Project in VS Code**: Open the entire `multi-modal-rag-cheme` folder in Visual Studio Code.
3.  **Select the Python Kernel**:
    * Open the `RAG_Notebook.ipynb` file.
    * Click the "Select Kernel" button in the top-right corner of the notebook editor.
    * From the dropdown list, choose the Python interpreter associated with your virtual environment (it should include `./venv/bin/python`).
4.  **Run the Notebook**: With the correct kernel selected, you can now run the cells sequentially to process your document and query the RAG system.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
