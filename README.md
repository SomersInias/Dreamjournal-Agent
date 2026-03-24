# Dream Journal Agent (LangChain + LangGraph)

A showcase project demonstrating how I implemented the information from the course **Foundation: Introduction to LangGraph - Python**,  to build a **tool-using AI agent** with **LangChain** and **LangGraph**, centered around a practical and personal use case: a **Dream Journal Assistant**. Personally I am deep facinated by dreams and spend time storing my dreams in my own dream journal. This seemed like a interesting project to see how these tools could enhance a digital stored dream journal.

##  Overview

The Dream Journal Agent helps users:
-  Record and transcribe dreams  
-  Store dreams in a structured journal
-  Search online for dream interpretation 
-  Retrieve and search past dreams  
-  Ask questions about dreams inside your dreamjournal  

This project showcases how an AI agent accessing tools can be useful as a sort of dreamjournal assistant. 

---

##  Features

###  Tool-Using Agent
The agent uses **LangChain tool calling** to dynamically decide when to:
- Transcribe audio
- Record audio
- Search the web
- Store dreams
- Retrieve past entries
- Answers questions about your dreamjournal

---

###  Audio Recording + Transcription
- Record dreams via a simple demo python code that allows audio recording in google colab.
- Transcribe happens by using **Whisper**  

---

###  Dream Journal Storage
- Dreams are stored in a `.txt` file to keep it simple for this demo project 
- Automatically:
  - Numbers entries  
  - Adds dates  
  - Generates titles (if not provided)  

---

###  Retrieval-Augmented Generation (RAG)
- Converts the dream journal into a vector database  
- Uses OpenAI embeddings (`text-embedding-3-large`)  
- Enables semantic search over past dreams  

---

###  Web Search Integration
- Uses **Tavily Search API**  
- Agent can search online for potential dream interpretation

---

###  Memory (Conversation History)
- Implemented using **LangGraph MemorySaver**  
- Enables:
  - Multi-turn conversations  
  - Context awareness  
  - Persistent interaction per thread (user)  

---

###  Agent Loop (LangGraph)
Built using a **ReAct-style loop**:

1. User input  
2. Agent reasoning  
3. Tool execution (if needed)  
4. Continue until final answer  

---

###  Observability (LangSmith)
- Integrated **LangSmith Studio** for tracing and debugging  
- Enables:
  - Inspection of agent decisions and tool calls  
  - Step-by-step execution tracking  
  - Easier debugging and evaluation of agent behavior  

This highlights how the system can be monitored and improved in a **production-like environment**.


---

##  Example Use Cases

- “Ask to Record youself explaining or reading your dream“  
- “Ask to Transcribe your recording so that there is a text version of the recording”  
- “Ask to Add the dream to your Dreamjournal”  
- “Ask the agent if you have dreams about a specific topic?”  
- “Ask it to Search online what falling dreams mean”  

---

##  How It Works

1. User sends a message  
2. Agent decides:
   - Respond directly  
   - OR call a tool  
3. Tool executes  
4. Result is fed back into the agent
5. Respond to the user 
6. Memory stores the interaction  


