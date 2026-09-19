# Embeddings with Neo4j

A technical implementation for document chunking, local embeddings and vector similarity search with Neo4j.

## Attribution

This repository is based on external source material published by UNIPDS and Erick Wendel.

Upstream material:
https://github.com/unipds-engenharia-de-ia-aplicada/engenharia-de-software-com-ia-aplicada

I keep the original author metadata in the package deliberately. This repository represents my technical implementation and evaluation of the example, not original authorship of the base material.

## What the code does

The current flow:

1. Loads a PDF document.
2. Splits it into overlapping chunks.
3. Generates embeddings with Hugging Face Transformers through LangChain.
4. Connects to Neo4j.
5. Stores document chunks in a vector index.
6. Executes similarity searches for predefined questions.
7. Prints the closest chunks for each query.

## Architecture

```text
PDF
 |
 v
Document processor
 |
 v
Text chunks
 |
 v
Embedding model
 |
 v
Neo4j vector index
 |
 v
Similarity search
```

## Requirements

- Node.js 22.13.1 or compatible
- Docker and Docker Compose
- Enough local memory to load the selected embedding model

## Environment

Create a `.env` file based on:

```env
NEO4J_URI=neo4j://localhost:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=password
EMBEDDING_MODEL=Xenova/all-MiniLM-L6-v2

OPENROUTER_API_KEY=
NLP_MODEL=
OPENROUTER_SITE_URL=
OPENROUTER_SITE_NAME=
```

The OpenRouter variables are present in the configuration layer but are not required by the current similarity-search flow in `src/index.ts`.

## Run

Start Neo4j:

```bash
npm run infra:up
```

Install dependencies:

```bash
npm ci
```

Run the ingestion and search flow:

```bash
npm start
```

Stop the local infrastructure:

```bash
npm run infra:down
```

## Current scope

This project demonstrates vector ingestion and semantic similarity search. It is not presented as a complete production RAG system.

A production implementation would still need concerns such as document identity, incremental indexing, access control, evaluation, retry policies, observability and lifecycle management.


## License and distribution

The upstream source repository is published under CC BY-NC-ND 4.0. Its LICENSE.md states that modified or adapted versions may not be distributed under the NoDerivatives condition. This repository is therefore not presented as a permissively licensed open-source derivative. See [NOTICE.md](NOTICE.md) for the provenance and licensing note.
