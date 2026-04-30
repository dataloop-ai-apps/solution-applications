# Custom CLIP & Ollama *RAG* Pipeline

### Introduction:

A customized variant of the CLIP + Ollama RAG solution with three differences:

1. **Empty datasets at install time** — both the source dataset (`Source Dataset`) and the chunks dataset (`Chunks Dataset`) are created empty. There is no preloaded corpus.
2. **Auto-ingest trigger** — an `Item.Created` trigger on the source dataset (DQL filter `metadata.system.mimetype == 'application/pdf'`) starts the preprocess pipeline automatically whenever a PDF is added, so chunks and embeddings are produced on the fly.
3. **Pipeline services scaled to 1 replica** — every pipeline dependency (CLIP, Ollama server, hosted chat completion, RAG and RAG-preprocessing templates) is configured with `minReplicas=1, maxReplicas=1` so a warm replica is always available.

The solution still uses CLIP for embeddings and the Dataloop hosted LLM (`phi4-mini:latest`) served via an Ollama server.

### Configuration:

Before publishing/installing, set the `app_id` on the `hosted-chat-completion` model configuration in `retrieval_pipeline_solution/dataloop.json` (placeholder `<APP_ID_TO_BE_SET>`).

### Installation:

In order to use the template, follow these steps:

* Open the pipelines page and select Create Pipeline.
* Select Use a Template from the dropdown list.

<img src="assets/pipeline_create.png" alt="Image of the pipeline creation page">

* In the search bar, type `Custom CLIP & Ollama RAG`, select the app and click install.
* Once the template is installed, click on *Create Pipeline*.
* Drop one or more PDFs into the *Source Dataset* — the preprocess pipeline will run automatically.
