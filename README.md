# SciPhi r2r

SciPhi r2r (RAG to Riches) is a Python framework designed for the rapid construction and deployment of production-ready Retrieval-Augmented Generation (RAG) systems. This semi-opinionated framework accelerates the transition from experimental stages to production-grade RAG systems.

## Installation

This project uses Poetry for dependency management. To install the project, you need to have Poetry installed on your system. If you don't have it, you can install it by following the instructions on the [official Poetry website](https://python-poetry.org/docs/#installation).

Once you have Poetry installed, you can install the project dependencies by running:

```bash
# git clone git@github.com:SciPhi-AI/sciphi_r2r.git && cd sciphi_r2r

poetry install
```

## Demonstration

https://github.com/SciPhi-AI/sciphi_r2r/assets/68796651/c648ab67-973a-416a-985e-2eafb0a41ef0



This will create a virtual environment and install all the necessary dependencies.

## Core Abstractions

The framework primarily revolves around three core abstractions:

- The **Ingestion Pipeline**: This provides methods for processing data, parsing files, and parsing entries. The abstraction can be found in [`ingestion.py`](sciphi_r2r/core/pipelines/ingestion.py).

- The **Embedding Pipeline**: This utilizes a `DatasetProvider` for input data, an `EmbeddingProvider` for generating embeddings, and a `VectorDBProvider` for storing these embeddings. The abstraction can be found in [`embedding.py`](sciphi_r2r/core/pipelines/embedding.py).

- The **RAG Pipeline**: This combines an `EmbeddingProvider`, `VectorDBProvider`, and a `LLMProvider` to process input queries or context and generate outputs based on the retrieved context. The abstraction can be found in [`rag.py`](sciphi_r2r/core/pipelines/rag.py).

Each pipeline incorporates a logging database for operation tracking.

## Running the Examples

The project includes several basic examples that demonstrate application deployment and standalone usage of the embedding and RAG pipelines:

1. [`app.py`](examples/basic/app.py): This example runs the main application, which includes the ingestion, embedding, and RAG pipelines served via FastAPI.

    ```bash
    poetry run uvicorn examples.basic.app:app
    ```


2. [`test_client.py`](examples/client/test_client.py): This example should be run after starting the main application. It demonstrates a test of the user client.

    ```bash
    poetry run python -m examples.client.test_client
    ```



3. [`rag_pipeline.py`](examples/basic/rag_pipeline.py): This standalone example demonstrates the usage of the RAG pipeline. It takes a query as input and returns a completion generated by the OpenAI API.

    ```bash
    poetry run python -m examples.basic.rag_pipeline
    ```

4. [`embedding_pipeline.py`](examples/basic/embedding_pipeline.py): This standalone example demonstrates the usage of the embedding pipeline. It loads datasets from HuggingFace, generates embeddings for the data using the OpenAI API, and stores the embeddings in a PostgreSQL vector database.


    ```bash
    poetry run python -m examples.basic.embedding_pipeline
    ```
