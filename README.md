# rag-chatbot

This document describes how the RAG application must be set up correctly in this repository and what preparations must be made.

## Prerequisites



## Setup Guide: RAG Chatbot – Swiss Law Assistant
1. Clone the Repository
 
git clone <REPOSITORY_URL>
cd rag-chatbot
 
2. Add API Key
 
Rename the environment file and add your Together.ai API key:
 
mv .env.apiKey .env
 
Then edit the .env file and insert your API key:
 
TOGETHER_API_KEY=your_actual_api_key_here
 
3. Build and Start the App
 
Use Docker Compose to build and launch all services:
 
docker-compose up --build
 
This sets up:
 
    🧠 ollama (local embedding model)
 
    📚 chroma (vector DB)
 
    🌐 Streamlit UI
 
4. Import Embeddings
 
Once containers are running (see that the app is live on http://localhost:8501), open a new terminal tab and run:
 
docker exec -it rag_chatbot_app python scripts/import_embeddings_to_chroma_server.py
And then:
docker exec -it ollama ollama pull nomic-embed-text
 
You should see logs like:
 
✅ Importiert: ZGB.txt
✅ Importiert: OR.txt
🎉 Import abgeschlossen: 2800 Embeddings in Chroma (Server-Modus)
 
5. Use the App
 
Open http://localhost:8501 in your browser. You can now ask legal questions like:
 
    Welche Regelungen gelten bei der Kündigung eines Mietvertrags?
 
ℹ️ Notes
 
    You only need to import embeddings after rebuilding (--build) or clearing the Chroma volume.
 
    Do not push data/chroma/ to Git – it’s excluded automatically.
 
    If you accidentally stop the app:
 
docker-compose up
