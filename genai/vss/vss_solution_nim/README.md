# NIM *VSS* Pipeline: Video Search & Summarization

### Introduction:

This VSS solution creates a template for video search and summarization pipelines powered by NVIDIA NIM. With this
approach, you can ingest video content, extract visual descriptions and audio transcripts, build a knowledge graph, and
query the processed content using natural language.

**Preprocessing Pipeline:**
- Splits videos into 15-second segments
- Visual branch: VILA VLM generates search-friendly video descriptions
- Audio branch: Parakeet ASR transcribes speech to text
- Embeds all text chunks using NIM Llama 3.2 NeMoRetriever
- Builds a knowledge graph via LLM entity/relationship extraction (Graph RAG)

**Retrieval Pipeline:**
- Queries the knowledge graph for relevant entities and relationships
- Performs vector search over embedded video descriptions and transcripts
- Generates answers grounded in the retrieved video context using NIM LLM

### Installation:

In order to use the template, you need to follow these steps:

* Open the pipelines page and select Create Pipeline.
* Select Use a Template from the dropdown list.
* In the search bar, type `NIM VSS Blueprint`, select the app and click install.
* Once the template is installed, click on *Create Pipeline*.
