# Conversational Search App (GPU required)

<img src="stablebeluga.png" alt="Stable Beluga" style="max-width: 100%; max-height: 100px;">

This repo contains code to build a conversational search application using LangChain and Streamlit. The application allows the user to have a conversational dialog with an AI assistant to find answers to their questions from a document collection.

**Note:** I have only tested this application on a machine with 24GB of RAM. Running the FAISS index and Beluga model uses around 15GB of memory with GPU acceleration enabled. So you will need a decently powered machine with a GPU to run this application smoothly.

## Overview

The application is built using the following main components:

- **Retriever**: Uses a FAISS index of vector embeddings of the document collection to retrieve relevant documents. The embeddings are created using the SentenceTransformers library.
- **Reader**: Uses the Stable Beluga model from Stability AI via HuggingFace Pipelines to read the retrieved documents and summarize an answer.
- **Frontend**: Built with Streamlit to handle the conversational flow - prompting the user for questions, displaying chat history, sending questions to the retriever/reader, and displaying answers.

## Setup

To run the application yourself, follow these steps:

1. Clone the repo
    
2. Create a conda environment from environment.yml
    
    ```bash
    conda env create -f environment.yml
    ```
    
3. Add the files in .txt or .html format to the ./docs folder so that the vector db works.
    
4. Run the dataprep.py script to get the embeddings.

    ```bash
    python dataprep.py
    ```
    
5. Run the Streamlit app
    
    ```bash
    streamlit run streamlit_app.py --server.address 0.0.0.0 --server.port 8080 --server.fileWatcherType none --browser.gatherUsageStats False
    ```
    

This will start the Streamlit app on port 8080.

## Files

- `dataprep.py` - Script to generate FAISS index from the document collection
- `retrieve_from_beluga.py` - Functions to build the conversational retrieval chain
- `streamlit_app.py` - Streamlit application
- `environment.yml` - Conda environment specification
- `.env` - Environment variables