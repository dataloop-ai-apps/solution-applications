# Onboarding Complete Dataloop Solutions Repository

## Solutions

---

### 1. [Active Learning for Agriculture: Seedlings](mlops/active_learning/active_learning_seedlings/README.md)

> **Usecase:** A precision agriculture company needs to classify crop seedlings vs weeds across thousands of field images to automate early-stage weed removal.

> **Problem:** Labeling field images is expensive and slow. The model needs to improve continuously as new field data arrives daily, but the annotation budget is limited — they can only label the most impactful samples.

**Components:**
| Type | Description |
|------|-------------|
| Pipeline | Active learning loop (pre-annotate → uncertainty scoring → human review → retrain) |
| Dataset | Raw un-annotated field images (Seedlings) |
| Dataset | Ground-truth annotated dataset (grows each iteration) |
| Models | 3 trained models with increasing GT data (snapshots after active learning iterations) |

**Show:**
- Data keeps flowing in, latest model pre-annotates before human-in-the-loop review
- Model training — cron/manual activation of the training loop
- Model comparison — models keep improving after each iteration, measurable accuracy gains

---

### 2. [RAG Over Recipes Data (OpenAI)](genai/rag/rag_solution_recipes/README.md)

> **Usecase:** A food & recipe platform wants to let users ask natural-language questions (*"What's a gluten-free Italian dessert?"*) and get accurate answers grounded in their proprietary recipe collection.

> **Problem:** The recipe catalog lives in unstructured PDFs and documents with mixed text and images. A plain LLM hallucinates recipes or misses ingredients — the answers must be grounded in the actual source documents.

**Components:**
| Type | Description |
|------|-------------|
| Pipeline | RAG multi-modal preprocess pipeline (PDF parsing, chunking, embedding) |
| Pipeline | RAG retrieve & generate flow (query → retrieve → LLM answer) |
| Dataset | Raw PDFs and documents (recipe collection) |
| Dataset | Preprocessed chunks with extracted features and embeddings |
| Models/Apps | OpenAI embedder, OpenAI LLM, vector store |

**Show:**
- End-to-end ingestion of new recipe documents into the knowledge base
- Natural-language Q&A with source attribution back to specific recipe chunks
- Multi-modal handling — extracting information from both text and images in recipes

---

### 3. RAG Blueprint: Knowledge-Base from Banking PDFs

> **Usecase:** A retail bank needs an internal assistant that helps loan officers instantly find answers about mortgage policies, compliance rules, and product terms buried across hundreds of regulatory documents.

> **Problem:** Loan officers waste hours searching through dense banking PDFs for policy details. Answers are scattered across multiple documents, and incorrect interpretations risk compliance violations.

**Components:**
| Type | Description |
|------|-------------|
| Pipeline | RAG multi-modal preprocess pipeline (PDF parsing, chunking, embedding) |
| Pipeline | RAG retrieve & generate flow (query → retrieve → LLM answer) |
| Dataset | Raw PDFs and documents (mortgage policies, banking regulations, product guides) |
| Dataset | Preprocessed chunks with extracted features and embeddings |
| Models/Apps | Embedder, LLM, vector store |

**Show:**
- Ingesting and indexing a corpus of banking/mortgage documents
- Compliance-aware Q&A — *"What are the income requirements for a jumbo mortgage?"*
- Source traceability — every answer links back to the exact document and section

---

### 4. Metadata Enrichment for Autonomous Vehicles

> **Usecase:** An autonomous vehicle company collects millions of dashcam images daily and needs to automatically triage and quality-score them before they enter the annotation pipeline.

> **Problem:** Most raw captures are unusable — too dark, blurry, or duplicated. Sending everything to human annotators wastes budget. The team needs automated quality filtering and metadata tagging to route only valuable frames to labeling.

**Components:**
| Type | Description |
|------|-------------|
| Pipeline | Image processing with EXIF extraction, darkness scoring, and blurriness detection |
| Dataset | Dashcam and vehicle images (driving scenarios, varying conditions) |
| FaaS Nodes | Custom quality-score functions (brightness, blur, GPS/time extraction) |

**Show:**
- Automatic metadata enrichment on ingestion — every image gets quality scores and EXIF tags
- Filtering and smart routing — only images above quality thresholds proceed to annotation
- Dashboard view of dataset quality distribution (dark vs clear, sharp vs blurry)

---

### 5. PII Data Extraction with Microsoft Presidio — Healthcare

> **Usecase:** A healthcare organization needs to process patient intake forms and clinical notes, but must detect and redact personally identifiable information (PII) before the data can be used for research or ML training.

> **Problem:** Medical documents contain sensitive PII (names, SSNs, phone numbers, medical record IDs) mixed with clinically valuable text. Manual redaction is slow, error-prone, and doesn't scale — a single missed field is a HIPAA violation.

**Components:**
| Type | Description |
|------|-------------|
| Pipeline | Document ingestion → PII detection (Presidio) → redaction/masking → clean output |
| Dataset | Synthetic medical documents (patient forms, clinical notes, discharge summaries) |
| Models/Apps | Microsoft Presidio NER for PII detection, custom recognizers for medical IDs |

**Show:**
- Automatic detection and highlighting of PII entities in medical documents
- Side-by-side view: original vs redacted document
- Confidence scores per entity — human review only for low-confidence detections

---

### 6. Multimodal Indexing — NVIDIA Blueprint (Video, Audio, Images)

> **Usecase:** A media company needs to make their massive archive of raw video footage searchable — find specific scenes, spoken phrases, or objects across thousands of hours of unstructured video content.

> **Problem:** Video content is opaque to search — you can't ctrl+F a video. Manually tagging and cataloging footage is impossibly slow. The archive grows daily with new shoots, interviews, and field recordings that sit unused because no one can find what they need.

**Components:**
| Type | Description |
|------|-------------|
| Pipeline | Multimodal indexing (video → frame extraction → object detection + summarization + audio transcription) |
| Dataset | Raw video files (mixed content — interviews, field footage, events) |
| Model (NIM) | Open-world object detection (identify objects/scenes in frames) |
| Model (NIM) | Video summarization (generate scene-level text summaries) |
| Model (NIM) | Audio extraction and transcription (speech-to-text from video audio tracks) |

**Show:**
- End-to-end video ingestion — upload a video, get it indexed across all modalities
- Cross-modal search — *"Find clips where someone mentions 'product launch' near a whiteboard"*
- Rich metadata per video segment: detected objects, transcript, and scene summary

---

### 7. Data Indexing for Visualization and Understanding — Embedding + Clustering + Semantic Search

> **Usecase:** A data science team has a large image dataset (e.g. retail product photos, satellite imagery, or medical scans) and needs to explore, understand, and curate it visually before building models — without manually browsing thousands of items.

> **Problem:** Raw datasets are a black box — duplicates, outliers, class imbalances, and mislabeled items hide in plain sight. Without a way to visualize the data distribution and semantically search it, teams train on dirty data and waste cycles debugging model failures that are actually data failures.

**Components:**
| Type | Description |
|------|-------------|
| Dataset | Domain-specific image dataset with pre-extracted feature embeddings |
| Models/Apps | Embedder model (e.g. CLIP, ResNet) for feature extraction |

**Show:**
- Visual cluster map — explore the dataset as a 2D/3D embedding space, spot outliers and duplicates
- Semantic search — *"Find all images similar to this one"* using natural language or an example image
- Interactive curation — select clusters, invert selection, create annotation tasks, clone subsets for experiments

---

## Contributions, Bugs and Issues - How to Contribute

We welcome anyone to help us improve this app.  
[Here](CONTRIBUTING.md) are detailed instructions to help you report a bug or submit a feature request.
