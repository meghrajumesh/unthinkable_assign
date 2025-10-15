
## Local RAG Pipeline for PDF Q&A

Local RAG for PDF Question-Answering
This project demonstrates a complete Retrieval-Augmented Generation (RAG) pipeline that runs entirely on your local machine. It uses LangChain for orchestration, Ollama to serve local large language models (LLMs), and ChromaDB for in-memory vector storage. The primary goal is to allow users to ask questions about the content of one or more PDF documents securely and without relying on external APIs.

Table of Contents
Features

How It Works

Prerequisites

Installation

Usage

Project Structure

License

Features
100% Local Execution: All components, from embedding generation to language model inference, run locally. No data ever leaves your machine.

PDF Document Support: Easily load and process text from local PDF files.

Efficient Retrieval: Utilizes a vector database (ChromaDB) for fast and relevant context retrieval.

Flexible Model Support: Powered by Ollama, allowing you to easily swap out different open-source LLMs.

Advanced Retrieval Strategy: Implements a Multi-Query Retriever to generate multiple perspectives on a user's question, improving the quality of retrieved documents.

How It Works
The pipeline follows these core steps:

Load: The PDF document is loaded and its text content is extracted using UnstructuredPDFLoader.

Split: The extracted text is broken down into smaller, manageable chunks using RecursiveCharacterTextSplitter.

Embed: Each text chunk is converted into a numerical vector representation (embedding) using a local model (nomic-embed-text) served by Ollama.

Store: These embeddings are stored in a Chroma vector database for efficient similarity searching.

Retrieve: When a user asks a question, the Multi-Query Retriever uses an LLM (llama3.2) to generate several variations of the question. It then retrieves the most relevant text chunks from the vector database for all these variations.

Generate: The original question and the retrieved context are passed to the language model (llama3.2), which generates a final, context-aware answer.

Prerequisites
Before you begin, ensure you have the following installed on your system:

Python (version 3.8 or higher)

Git

Ollama: Make sure the Ollama application is running in the background.

Installation
Follow these steps to set up the project environment.

Clone the Repository

Bash

git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
Install Python Dependencies
It is recommended to use a virtual environment.

Bash

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

# Install the required packages
pip install -r requirements.txt
Pull Required Ollama Models
This project uses llama3.2 for generation and nomic-embed-text for embeddings. Open your terminal and run the following commands:

Bash

ollama pull llama3.2
ollama pull nomic-embed-text
You can confirm the models are installed by running ollama list.

Usage
Add Your PDF: Place the PDF file you want to query into the root directory of the project.

Update the Notebook: Open the unthinkable_assignment.ipynb file. In the third code cell, update the local_path variable to match your PDF's filename.

Python

# Find this line and change the filename
local_path = "your_document_name.pdf"
Run the Notebook: Execute the cells in the notebook from top to bottom.

The initial cells will handle installations and imports.

The PDF loading and embedding process may take a few moments depending on the size of your document and your machine's performance.

The final cell will prompt you for input.

Ask a Question: Type your question into the input box provided by the last cell and press Enter. The model will generate an answer based on the content of your PDF.

Project Structure
.
├── unthinkable_assignment.ipynb  # The main Jupyter Notebook containing the RAG pipeline.
├── requirements.txt              # A list of all Python dependencies.
├── README.md                     # This documentation file.
└── .gitignore                    # Specifies files for Git to ignore.
