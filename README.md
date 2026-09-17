# 🎤 VoxGraph

VoxGraph is a full-stack AI application that converts audio content (speech) into a **structured knowledge graph**. Users provide a public audio URL, and the app:

1. Transcribes the audio using **Mistral Voxtral**.
2. Extracts entities and relations with **Mistral chat models**.
3. Builds and renders a knowledge graph using **React + Cytoscape**.

---
<img width="955" height="276" alt="image" src="https://github.com/user-attachments/assets/1fc8014e-b920-4b51-afe9-5a7b26dd2948" />

---
## 🎯 Product Vision
VoxGraph addresses a critical bottleneck in AI development: the shortage of high-quality, structured training data. While audio content is abundant in the form of podcasts, interviews, lectures, meetings, this unstructured information cannot be directly used to train modern AI systems that power recommendations, search, and reasoning.
VoxGraph transforms audio into graph-structured training data, unlocking a valuable data source for downstream AI tasks. Knowledge graphs are among the most effective representations for:

Recommendation Systems: Entity-relation graphs power collaborative filtering and content discovery
Question Answering: Graph structures enable multi-hop reasoning
Information Retrieval: Semantic relationships improve search relevance
Knowledge Base Construction: Automatically building structured databases from unstructured sources 

Beyond creating training data, VoxGraph enables users to understand complex relationships and navigate information spatially, making implicit connections explicit and searchable. 

---

## 💡 Problem Statement
### The Challenge

Data Scarcity for AI: High-quality labeled training data is expensive and time-consuming to create
Unstructured Audio Abundance: Millions of hours of audio content remain untapped as potential training data
Graph Structure Demand: Modern AI systems (GNNs, recommendation engines, RAG systems) require graph-formatted data
Manual Annotation Costs: Human labeling of entities and relationships doesn't scale
Limited Data Diversity: Existing graph datasets are domain-specific and insufficient for general AI training

### The Solution
VoxGraph automates the creation of graph-structured training datasets from audio:

Intelligent Transcription: Leveraging Mistral's Voxtral model for accurate speech-to-text
Smart Entity Extraction: AI-powered identification of key concepts, people, and topics
Relationship Mapping: Automatic detection of connections between entities from the audio
Export-Ready Formats: Generate training datasets compatible with GNN frameworks, recommendation systems, and knowledge base pipelines

---

## 🧰 Tech Stack

- **Backend**: FastAPI, Python, Requests  
- **Frontend**: React, Vite, Cytoscape.js  
- **AI Models**: Mistral Voxtral for audio transcription, Mistral chat models for entity/relation extraction  
- **Deployment**: Local development (can be extended to cloud)

---

## ⚡ Features

### Core Functionality
| Feature | User Benefit | Technical Implementation |
|---------|-------------|-------------------------|
| **Audio Input** | Supports any public `.mp3` or `.wav` URL | HTTP request validation + streaming |
| **AI Transcription** | 95%+ accuracy across accents using Voxtral | Mistral Voxtral API integration |
| **Entity Extraction** | Automatically identifies people, organizations, concepts | LLM-powered NER with Mistral chat models |
| **Relationship Detection** | Discovers connections between entities | Prompt-engineered relation extraction |
| **Graph Visualization** | Interactive, zoom/pan-enabled knowledge maps | React + Cytoscape.js rendering |
| **Training Data Export** | Export graphs in formats for GNNs, recommendation systems | JSON/CSV/GraphML serialization (roadmap) |
| **Real-time Processing** | Complete pipeline in seconds | Async FastAPI backend |

---

## Differentiators

✅ Training Data Pipeline: Purpose-built for creating AI training datasets, not just visualization
✅ Zero Manual Annotation: Fully automated entity-relation extraction
✅ Scalable Data Creation: Process hundreds of audio files into training graphs
✅ ML-Ready Outputs: Export formats compatible with PyTorch Geometric, DGL, Neo4j
✅ Privacy-First: Process publicly accessible content without data retention
✅ Modern Stack: Production-ready technologies (FastAPI, React, Vite)

---

## 👥 Target Users
Primary Personas

AI/ML Engineers: Building training datasets for recommendation systems, GNNs, and knowledge graphs
Data Scientists: Creating structured datasets for NLP and knowledge base applications
ML Research Teams: Generating graph-structured data for novel AI architectures
AI Startups: Bootstrapping training data without expensive manual annotation
Researchers & Academics: Analyzing interview data, lectures, and oral histories for qualitative research

Use Cases
Primary: Training Data Generation

Graph Neural Network (GNN) training datasets
Recommendation system knowledge graphs (user-item-attribute relationships)
Retrieval-Augmented Generation (RAG) knowledge bases
Question answering system training data
Entity linking and relation extraction benchmarks

Secondary: Knowledge Work

Interview analysis and qualitative research
Podcast content summarization and indexing
Meeting intelligence and relationship mapping
Investigative journalism connection discovery

---

## 📦 Setup Instructions

### 1. Clone the repository

git clone <your-repo-url>
cd vox_graph

### 2. Backend Setup

Navigate to the backend folder:

cd backend

Create a virtual environment (optional but recommended):

python -m venv venv
source venv/bin/activate    # macOS/Linux
venv\Scripts\activate       # Windows

Install dependencies:

pip install -r requirements.txt

Create a .env file in backend/ with your Mistral API key:

MISTRAL_API_KEY=<your-mistral-api-key>

Run the backend:

uvicorn backend.application:app --reload

Runs on http://localhost:8000 by default.

### 3. Frontend Setup

Navigate to the frontend folder:

cd ../frontend

Install dependencies:

npm install

Run the frontend:

npm run dev

Opens on http://localhost:5173.

### 📝 Usage

Open your browser to http://localhost:5173.

Paste a publicly accessible audio URL (.mp3 or .wav).

Click “Build Knowledge Graph”.

Wait a few seconds — the transcript and graph will appear.

Tip: Use raw GitHub URLs for audio files. Example:
https://raw.githubusercontent.com/username/repo/main/audio.mp3

---
## 📊 Product Metrics & Success Criteria
Key Performance Indicators (KPIs)
Processing Performance

Processing Speed: < 30 seconds for 5-minute audio
Transcription Accuracy: > 95% WER (Word Error Rate)
Entity Extraction Precision: > 85% relevant entities
Relation Extraction Recall: > 80% of meaningful relationships captured

Training Data Quality

Graph Density: Average edges per node (target: 2-5 for quality training data)
Entity Diversity: Unique entity types per graph
Schema Consistency: % of graphs following standardized entity/relation types
Export Success Rate: % of graphs successfully converted to ML formats

User Engagement

Graphs created per user session
Average graph size (nodes + edges)
Export/download rate (indicates training data usage)

System Reliability

99%+ uptime for processing pipeline
API response time < 2s (excluding AI model latency)

Future Roadmap Validation 

ML Engineer Surveys: Export format preferences, integration pain points
A/B Testing: Graph quality heuristics, entity type schemas
Usage Analytics: Most common audio sources, graph patterns, export formats


---
## ⚙️ Configuration

CORS is enabled for * origins in application.py.

Update the Voxtral model in mistral_client.py:

MODEL = "voxtral-mini-latest"

Ensure your audio URL is publicly accessible — private links will fail.

🚀 Project Structure
```bash
vox_graph/
├── backend/
│   ├── application.py        # FastAPI backend
│   ├── models.py             # Pydantic models
│   ├── graph_builder.py      # Graph construction logic
│   ├── mistral_client.py     # Voxtral + Mistral API calls
│   
├── frontend/
│   ├── app.jsx               # Main React app
│   ├── api.js                # Axios calls to backend
│   ├── graph.jsx             # Cytoscape graph rendering
│   ├── main.jsx              # React entrypoint
│   ├── styles.css            # Styling
│   └── vite.config.js        # Vite config
└── README.md
⚠️ Notes

The app requires public URLs for audio files. Private storage services may fail.

Backend calls Mistral’s Voxtral model — ensure you have a valid API key.

The transcription and entity/relation extraction can take a few seconds per audio.

📄 License

MIT License © 2026





