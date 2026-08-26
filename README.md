# Agentic RAG

A notebook-based retrieval-augmented generation (RAG) demo. The project loads PDF documents, splits them into chunks, creates embeddings with `all-MiniLM-L6-v2`, stores them in ChromaDB, and queries the resulting collection.

## Project Structure

- `Notebook/document.ipynb` - LangChain document and text-loader examples.
- `Notebook/pdf_loader.ipynb` - PDF ingestion, chunking, embedding, vector-store, and retrieval pipeline.
- `data/pdfs/` - Source PDF documents used by the pipeline.
- `data/text_files/` - Sample text documents.
- `data/vector_store/` - Local ChromaDB output generated during ingestion.
- `requirements.txt` - Python dependencies.

## Setup

1. Create and activate a Python 3.12 environment.
2. Install the dependencies:

   ```powershell
   pip install -r requirements.txt
   ```

3. Create `Notebook/.env` with the credentials required by the query-generation cells:

   ```text
   GROQ_API_KEY=your_groq_api_key
   ```

   Do not commit `.env` files or API keys. If a real key has already been committed, revoke it and create a replacement.

## Running the Notebooks

Open the notebooks in VS Code and run `pdf_loader.ipynb` from the `Notebook` directory. Its relative paths expect the notebook working directory to be `Notebook`, with the source files in `../data`.

The ingestion cells create `data/vector_store/` automatically. Delete that directory and rerun the ingestion cells whenever the source documents or embedding configuration changes.

## Version Control

The vector store is generated data and should normally not be pushed to Git. Add this entry to `.gitignore`:

```gitignore
data/vector_store/
```

If it has already been committed, remove it from Git tracking without deleting the local files:

```powershell
git rm -r --cached data/vector_store
git add .gitignore
git commit -m "Ignore generated vector store"
git push
```

The source PDFs and notebooks are sufficient to rebuild the vector store.