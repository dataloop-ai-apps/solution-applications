# Custom CLIP & Ollama *RAG* Pipeline: Contracts

### Introduction:

This is a customized variant of the CLIP + Ollama Contracts RAG solution with three differences:

1. **Empty datasets at install time** — both the source PDF dataset and the chunks dataset are created empty. There are no preloaded CAUD contracts.
2. **Auto-ingest trigger** — an `Item.Created` trigger on the source dataset (DQL filter `metadata.system.mimetype == 'application/pdf'`) starts the preprocess pipeline automatically whenever a PDF is added, so chunks and embeddings are produced on the fly.
3. **Pipeline services scaled to 1 replica** — every pipeline dependency (CLIP, Ollama server, hosted chat completion, RAG and RAG-preprocessing templates) is configured with `minReplicas=1, maxReplicas=1` so a warm replica is always available.

The solution still uses CLIP for embeddings and the Dataloop hosted LLM (`phi4-mini:latest`) served via an Ollama server, exactly like the original `RAG template - Contracts`.

### Configuration:

Before publishing/installing, set the `app_id` on the `hosted-chat-completion` model configuration in `retrieval_pipeline_solution/dataloop.json` (placeholder `<APP_ID_TO_BE_SET>`).

### Installation:

In order to use the template, follow these steps:

* Open the pipelines page and select Create Pipeline.
* Select Use a Template from the dropdown list.

<img src="assets/pipeline_create.png" alt="Image of the pipeline creation page">

* In the search bar, type `RAG template - Custom Contracts`, select the app and click install.
* Once the template is installed, click on *Create Pipeline*.
* Drop one or more PDFs into the *CAUD Contracts Custom PDF Dataset* — the preprocess pipeline will run automatically.
