# ChemE GPT

### A Tool Born From Frustration

This Retrieval-Augmented Generation model was made out of frustration as a chemical engineering student. Unlike more popular majors like CS, ChemE has precious few resources to learn from outside the classroom. Our best bet is usually a 1,000-page textbook.

So, instead of spending another 8 hours on my thermodynamics homework looking for one very specific equation, I built this. This RAG system is designed to help me find information faster and give me better answers than traditional LLMs that hallucinate like crazy.

## File Structure

The repository is organized as follows:

```
multi-modal-rag-cheme
├── .gitignore
├── content              # Directory to hold your source PDF document (must be added by you)
│   └── YOUR_PDF_FILE.pdf
├── cheme_rag.ipynb
├── LICENSE
├── README.md
└── requirements.txt
```

## How It Works

The notebook executes a four-stage process to enable the RAG pipeline:

1.  **Document Parsing:** The system first parses a source PDF and uses the `unstructured.io` library to break it down into its constituent parts. It separates standard text paragraphs from tables and also extracts all visual elements like charts and diagrams.

2.  **Summarization:** To improve search accuracy, a summary is generated for every single piece of content. A text model, like `gemma2-9b-it`, summarizes the text and tables, while a vision model, like `gpt-4o-mini`, creates detailed descriptions for each image, plot, and diagram.

3.  **Vectorization:** The system uses LangChain's `MultiVectorRetriever` strategy. The summaries are converted into vectors using an embedding model, like `text-embedding-3-small`, and stored in a ChromaDB vector database, creating an efficient search index. The original, full-detail content (the actual text and images) is stored separately and linked to these summaries.

4.  **Generating Answer:** When you ask a question, the system searches the vector database to find the most relevant summaries. It then retrieves the original, full-resolution content associated with those summaries. This context, containing both text and images, is assembled into a prompt and sent to the multi-modal LLM to create a final, comprehensive answer.

## Technology Stack

* [**Azure AI Foundry:**](https://azure.microsoft.com/en-us/products/ai-foundry) Provides the core AI capabilities, including the multi-modal LLM for final answer generation and image analysis, and the embedding model for vectorizing the summaries.
  * **Approximate Cost:** In my development, for a ~700 page textbook, with ~650 vision requiring elements (images, diagrams, plots), it cost **$1.25** in API calls using `gpt-4o-mini` and `text-embedding-3-small` (P.S. students get $100 in free credits on [Azure](https://azure.microsoft.com/en-us/free/students)).
* [**LangChain:**](https://smith.langchain.com/) Acts as the primary framework to connect all the components, create the RAG pipeline, and implement the [`MultiVectorRetriever`](https://python.langchain.com/api_reference/langchain/retrievers/langchain.retrievers.multi_vector.MultiVectorRetriever.html) logic.
* [**Unstructured.io:**](https://docs.unstructured.io/open-source/core-functionality/partitioning#partition-pdf) The data parsing library for extracting and separating the text, tables, and images from the source PDF.
* [**Groq:**](https://console.groq.com/home) Used to access open source LLMs for summarization of all text-based content (don't need a paid vision model for text summaries).
* [**ChromaDB:**](https://docs.trychroma.com/docs/overview/getting-started) An open-source vector database that stores the summary embeddings and enables fast similarity searches.
* **VS Code + WSL:** The development and runtime environment for the project.

## Getting Started

Follow these instructions to set up your development environment. This assumes you are operating in a Linux-based environment such as Ubuntu (either natively or through WSL on Windows).

1. Clone the repository:
```bash
git clone https://github.com/km-kushmathur/multi-modal-rag-cheme.git
```

2. Enter the root folder:
```bash
cd multi-modal-rag-cheme
```

3. Install system-level dependencies:
```bash
sudo apt-get update && sudo apt-get install -y poppler-utils tesseract-ocr libmagic-dev
```

4. Create a virtual environment:
```bash
python3 -m venv venv
```

5. Activate the environment (must be done every time you start a new session)
```bash
source ./venv/bin/activate
```

## Disclaimer

This repository and notebook are provided as an example script intended only for local experimentation and educational purposes.

If you plan on sharing this code or uploading it to a public repository, please create an alternate `.env` file to safely store your API keys and ensure that file is added to your `.gitignore` to prevent accidental exposure of sensitive credentials.
