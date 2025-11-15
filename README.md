🤖 PersonaBot: The AI Chatbot That Learns from PDFs & Websites

PersonaBot is a "Retrieval-Augmented Generation" (RAG) chatbot that you can train on custom knowledge. It's designed to ingest information from multiple sources—including PDF documents and live website URLs—to create a centralized, chat-ready knowledge base.

You can use it to build a "Persona" of a public figure by feeding it their portfolio website, or create an "Expert" by feeding it technical documentation.

This project is built with Python, Streamlit, LangChain, and OpenAI.

✨ Features

Multi-Source Ingestion: Feed the bot knowledge from PDF files and public website URLs.

Web Scraper: A built-in loader scrapes and cleans text content from any provided URL.

PDF Processor: Automatically extracts and chunks text from uploaded PDF documents.

Vector "Memory": Uses ChromaDB as a local vector store to give the AI a persistent memory.

Simple Web UI: A clean, easy-to-use chat interface built with Streamlit.

⚙️ How It Works: The RAG Pipeline

Input: The user provides a source via the Streamlit UI (either a PDF upload or a URL string).

Load:

If PDF: PyPDFLoader reads the document.

If URL: WebBaseLoader (from LangChain) connects to the URL, scrapes the HTML, and parses the text content.

Split: The raw text from either source is passed to a RecursiveCharacterTextSplitter. This breaks the text into small, semantically related "chunks."

Embed: Each text chunk is converted into a numerical representation (a "vector embedding") using OpenAI's models. This vector captures the meaning of the text.

Store: These vectors are stored in a ChromaDB vector database on your local disk. This is the bot's permanent "brain."

Retrieve & Generate (The Chat Loop):

When you ask a question, your query is also converted into a vector.

The app searches the ChromaDB database for the most relevant text chunks from its memory (this is the "Retrieval").

These chunks (the "context") and your original question are sent to the LLM (e.g., GPT-3.5).

The LLM "Generates" a new, human-like answer based only on the context provided.

🛠️ Tech Stack

Python 3.10+

Streamlit: For the web interface.

LangChain: For the core RAG components (Loaders, Splitters, Chains).

OpenAI: For text embeddings and the chat model.

ChromaDB: For the local vector database.

BeautifulSoup4 & lxml: For web scraping (dependencies of WebBaseLoader).

pypdf: For reading PDF files.

python-dotenv: To manage your API key.

🚀 How to Run Locally

1. Clone the Repository:

git clone [https://github.com/YOUR_USERNAME/personabot.git](https://github.com/YOUR_USERNAME/personabot.git)
cd personabot


2. Create a Virtual Environment (Recommended):

python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate


3. Install Dependencies:

pip install -r requirements.txt


(You will need to create a requirements.txt file listing: streamlit, langchain, openai, chromadb, beautifulsoup4, lxml, pypdf, python-dotenv)

4. Set Up Your API Key:

Create a file named .env in the root folder.

Add your OpenAI API key to it:

OPENAI_API_KEY="sk-..."


5. Run the Streamlit App:

streamlit run app.py


Open your browser to http://localhost:8501 and start building your bot's brain!

A Note on LinkedIn: While this tool can scrape public blogs and portfolio sites, directly scraping linkedin.com is against their Terms of Service and is blocked by their security. For building a "persona", use a personal blog, a "About Me" page, or a news article about the person.
