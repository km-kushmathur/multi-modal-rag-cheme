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
├── notebooks/
│   └── RAG_Notebook.ipynb
├── .env.example
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

(This step is for others using your repo. You will connect your local folder to GitHub in a later step).

```bash
git clone https://github.com/YOUR_USERNAME/multi-modal-rag-cheme.git
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

The project requires API keys from Azure, Groq, and optionally LangChain for tracing.

```bash
# 1. Copy the example .env file
cp .env.example .env

# 2. Edit the .env file with your secret keys using a text editor
nano .env
```

Fill in the placeholders in the `.env` file with your actual credentials.

## How to Run

1.  **Place Your PDF**: Add the PDF file you want to process into the `content/` directory.
2.  **Launch Jupyter**: Make sure your `venv` is activated and run:
    ```bash
    jupyter notebook
    ```
3.  **Open and Run the Notebook**: In the Jupyter interface, navigate to the `notebooks/` directory and open `RAG_Notebook.ipynb`. Run the cells sequentially to process your document and query the RAG system.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
