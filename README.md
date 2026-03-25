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
- Create vector database of the dreamjournal
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
- Converts the dream journal into a vector database  (this is added as a seperate tool for the agent so that it can call it again if needed when new dreams are added into the dreamjournal) 
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

---

## Full Conversation example 


================================ Human Message ================================= <br>

Hey I had a great dream last night? <br>
================================== Ai Message ================================== <br>

That sounds wonderful! Would you like to share your dream with me? You can describe it in text, or if you prefer, you can record the details. Let me know what you'd like to do! <br>
================================ Human Message ================================= <br>

Hey I had a great dream last night, can I record it? <br>
================================== Ai Message ================================== <br>
Tool Calls:
  record_audio (call_9Lbp2pcgfxAPZA0AaSn2cq2C)
 Call ID: call_9Lbp2pcgfxAPZA0AaSn2cq2C
  Args: 
  <br>
================================= Tool Message ================================= <br>
Name: record_audio

Audio record tool successfully called <br>
================================== Ai Message ================================== <br>

I've set up the recording for you. Please go ahead and record your dream. Let me know when you're finished, and if you'd like, I can help transcribe it for you! <br>
================================ Human Message ================================= <br>

Can you transcribe this dream for me <br>
================================== Ai Message ================================== <br>
Tool Calls:
  transcribe (call_Yz038sAgCvbD6du9ou80qz6j)
 Call ID: call_Yz038sAgCvbD6du9ou80qz6j
  Args:
    audio_path: /content/recorded_audio.wav 
    <br>
================================= Tool Message ================================= <br>
Name: transcribe

 The dream was about I was talking to someone and in the background my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself. <br>
================================== Ai Message ================================== <br>

Here's your transcribed dream: <br>

"The dream was about I was talking to someone and in the background, my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself." <br>

Please read through it and let me know if any corrections are needed, like names or specific details that might have been transcribed incorrectly. <br>
================================ Human Message ================================= <br>

it looks good, can you add it to my dreamjournal? <br>
================================== Ai Message ================================== <br>

Could you please provide the path to your dream journal file so I can add this entry for you? <br>
================================ Human Message ================================= <br>

the path is /content/testdreamjournal2.txt <br>
================================== Ai Message ================================== <br>
Tool Calls:
  add_dream_to_dreamjournal (call_7m2PgDffgXfT26TZdQpeOvsy)
 Call ID: call_7m2PgDffgXfT26TZdQpeOvsy
  Args:
    dream_text: The dream was about I was talking to someone and in the background, my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself.
    file_path: /content/testdreamjournal2.txt
    title: Fire Phoenix Merge

<br>
================================= Tool Message ================================= <br>
Name: add_dream_to_dreamjournal <br>

Dream 12 added: 'Fire Phoenix Merge' (03/24/2026) <br>
================================== Ai Message ================================== <br>

Your dream titled "Fire Phoenix Merge" has been added to your dream journal. If there's anything else you'd like to do, feel free to let me know! <br>
================================ Human Message ================================= <br>

can you search online what this dream could mean? <br>
================================== Ai Message ================================== <br>
Tool Calls:
  search_web (call_QCx77rDodtC1I7In9hHdKRjO)
 Call ID: call_QCx77rDodtC1I7In9hHdKRjO
  Args:
    question: meaning of dreaming about a phoenix merging with oneself <br>
================================= Tool Message ================================= <br>
Name: search_web <br>

<Document href="https://www.auntyflo.com/dream-dictionary/phoenix">
# Phoenix Dream Meaning. ## What does a Phoenix mean in your dream? ## Phoenix. Seeing the phoenix in a dream is connected to rebirth, new starts, and new beginnings. The dream about a phoenix is a good omen. The phoenix in your dream is most probably a spiritual symbol, and therefore you should enjoy positive times ahead. ### In your dream you may have. To dream of phoenix is the omen of novelty in your life, and this could take the shape of renewal, transformation, or even immortality. Dreaming about a phoenix could also indicate that you did not finish processing your past, and that your past might continues to haunt you in the present. To dream about a phoenix bird changing shapes all the time it refers to changes in your life. To dream you witness a phoenix change into an object or a anything else it means a change in your health. ### Feelings that you may have encountered during a dream of phoenix.
</Document>
<br>
---

<Document href="https://tanyacasteel.com/project/phoenix-meaning/">
The Phoenix represents spiritual growth, not only in overcoming adversity but in rising with a heightened sense of self-awareness. When we face trials, we can
</Document>
<br>
---

<Document href="https://www.dreamdictionary.org/symbolism/phoenix-symbolism/">
## Phoenix Dream Meaning. So what is the meaning behind the **phoenix when it appears in our dreams**? The green phoenix in your dream governs your heart chakra suggesting you have opened or will undergo a powerful transformation. **Dreaming of a phoenix** and a wolf is a very powerful image of the starting phase of this inner transformation. I had a dream I entered a corridor where there were different types of colored phoenix, some were flying high some we’re flying in circles others perched on the railing some sitting some soaring, there was a long staircase that lead to a door, a red phoenix perched on the bottom of the staircase lead me to the wall on the side of the staircase and sat at the top of these vines that lead to the door so I climbed the vines and once I got to the top I opened the door to find a person looking out… Read more ». <br>
</Document>
================================== Ai Message ================================== <br>

Dreaming about a phoenix merging with oneself is often associated with themes of rebirth, transformation, and renewal. The phoenix is a powerful symbol of overcoming adversity and rising anew, which can indicate a period of personal growth or a significant change in your life. <br>

- The phoenix is linked to new beginnings and positive transformations. It might be a sign of spiritual growth and self-awareness, suggesting you're moving past challenges and stepping into a heightened state of existence. <br>

- This dream could also symbolize that you are not done processing a part of your past, or that you are undergoing or about to undergo an important transformation or renewal in your life. <br>

For more detailed interpretations, you can explore the articles linked above that delve into different aspects of what the phoenix represents in dreams. <br>
================================ Human Message ================================= <br>

can you search in my dreamjournal of I had another dream about a phoenix? <br>
================================== Ai Message ================================== <br>
Tool Calls:
  dreamjournal_to_vectordatabase (call_5qbDT6QHqXjbPQuXXul78ZiH)
 Call ID: call_5qbDT6QHqXjbPQuXXul78ZiH
  Args:
    file_path: /content/testdreamjournal2.txt <br>
================================= Tool Message ================================= <br>
Name: dreamjournal_to_vectordatabase <br>

null <br>
================================== Ai Message ================================== <br>
Tool Calls:
  retrieve_context_dreamjournal (call_DMXT7fwKt62Yf6w98xep7EB8)
 Call ID: call_DMXT7fwKt62Yf6w98xep7EB8
  Args:
    query: phoenix <br>
================================= Tool Message ================================= <br>
Name: retrieve_context_dreamjournal <br>

("Source: {'source': '/content/testdreamjournal2.txt'}\nContent: Dream 1: The Dog and the Bone\nDate: 12/05/2015\n\nI dream about a dog that gave me a bone.\n\n/end\n\nDream 2: The Floating Library\nDate: 03/18/2016\n\nI was in a giant library where all the books floated around me. When I opened one, I was pulled into the story itself. In one book, I was soaring through the clouds on the back of a golden eagle, feeling the wind rush past me.\n\n/end\n\nDream 3: Reverse City\nDate: 09/02/2016\n\nI walked through a city where everything was upside down. The roads were above my head, and people moved along the ceilings. When I touched certain objects, gravity flipped, and I fell upward instead of down.\n\n/end\n\nDream 4: Time-Travel Garden\nDate: 04/11/2017\n\nI wandered into a garden where each flower seemed to represent a different era. When I touched a rose, I found myself in ancient Rome, and a simple daisy sent me to a futuristic city full of glowing towers.\n\n/end\n\nDream 5: Ocean in the Sky\nDate: 08/27/2017\n\nI was swimming in a vast ocean suspended in the sky. Schools of glowing fish brushed past my face, and whales leapt gracefully from one cloud to another as the sunlight shimmered around me.\n\n/end\n\nDream 6: Endless Staircase\nDate: 01/19/2018\n\nI climbed a staircase that seemed to stretch on forever. Every landing transformed into something new—a dense jungle, a snowy mountain, a bustling marketplace—each more vivid than the last.\n\n/end\n\nDream 7: Mirror World\nDate: 06/05/2018\n\nI entered a room full of mirrors, but my reflections moved independently. One version of me waved and beckoned me into a parallel life where I had made different choices years ago.\n\n/end\n\nDream 8: Musical Forest\nDate: 10/22/2019\n\nI wandered through a forest where the trees hummed melodies and the flowers bloomed to the music. Every step I took changed the song, creating a kaleidoscope of color and sound around me.\n\n/end\n\nDream 9: Talking Animals City\nDate: 02/14/2020\n\nI found myself in a city where animals spoke my language. A fox ran a café, a raccoon drove a bus, and a wise old owl sold maps showing hidden secrets I had never known existed.\n\n/end\n\nDream 10: Vanishing Island\nDate: 07/30/2021\n\nI discovered an island that slowly dissolved into thin air. As it vanished, glowing bridges appeared, leading to new floating islands, each stranger and more beautiful than the one before.\n\n/end\n\nDream 11: Dream Market\nDate: 11/09/2022\n\nI wandered through a market where people traded memories, emotions, and fragments of dreams. I traded a memory of my happiest day for a dream where I was flying through a sky made entirely of candy-colored clouds.\n\n/end\n\nDream 12: Fire Phoenix Merge\nDate: 03/24/2026\n\nThe dream was about I was talking to someone and in the background, my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself.", [Document(id='a7663b69-c50d-46b4-b47e-82c26cca7e79', metadata={'source': '/content/testdreamjournal2.txt'}, page_content='Dream 1: The Dog and the Bone\nDate: 12/05/2015\n\nI dream about a dog that gave me a bone.\n\n/end\n\nDream 2: The Floating Library\nDate: 03/18/2016\n\nI was in a giant library where all the books floated around me. When I opened one, I was pulled into the story itself. In one book, I was soaring through the clouds on the back of a golden eagle, feeling the wind rush past me.\n\n/end\n\nDream 3: Reverse City\nDate: 09/02/2016\n\nI walked through a city where everything was upside down. The roads were above my head, and people moved along the ceilings. When I touched certain objects, gravity flipped, and I fell upward instead of down.\n\n/end\n\nDream 4: Time-Travel Garden\nDate: 04/11/2017\n\nI wandered into a garden where each flower seemed to represent a different era. When I touched a rose, I found myself in ancient Rome, and a simple daisy sent me to a futuristic city full of glowing towers.\n\n/end\n\nDream 5: Ocean in the Sky\nDate: 08/27/2017\n\nI was swimming in a vast ocean suspended in the sky. Schools of glowing fish brushed past my face, and whales leapt gracefully from one cloud to another as the sunlight shimmered around me.\n\n/end\n\nDream 6: Endless Staircase\nDate: 01/19/2018\n\nI climbed a staircase that seemed to stretch on forever. Every landing transformed into something new—a dense jungle, a snowy mountain, a bustling marketplace—each more vivid than the last.\n\n/end\n\nDream 7: Mirror World\nDate: 06/05/2018\n\nI entered a room full of mirrors, but my reflections moved independently. One version of me waved and beckoned me into a parallel life where I had made different choices years ago.\n\n/end\n\nDream 8: Musical Forest\nDate: 10/22/2019\n\nI wandered through a forest where the trees hummed melodies and the flowers bloomed to the music. Every step I took changed the song, creating a kaleidoscope of color and sound around me.\n\n/end\n\nDream 9: Talking Animals City\nDate: 02/14/2020\n\nI found myself in a city where animals spoke my language. A fox ran a café, a raccoon drove a bus, and a wise old owl sold maps showing hidden secrets I had never known existed.\n\n/end\n\nDream 10: Vanishing Island\nDate: 07/30/2021\n\nI discovered an island that slowly dissolved into thin air. As it vanished, glowing bridges appeared, leading to new floating islands, each stranger and more beautiful than the one before.\n\n/end\n\nDream 11: Dream Market\nDate: 11/09/2022\n\nI wandered through a market where people traded memories, emotions, and fragments of dreams. I traded a memory of my happiest day for a dream where I was flying through a sky made entirely of candy-colored clouds.\n\n/end\n\nDream 12: Fire Phoenix Merge\nDate: 03/24/2026\n\nThe dream was about I was talking to someone and in the background, my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself.')]) <br>
================================== Ai Message ================================== <br>

Your dream journal doesn't contain any previous dreams specifically mentioning a phoenix, except for the recent entry about the "Fire Phoenix Merge." If you'd like to explore other dreams or have any other questions, feel free to let me know! <br>
================================ Human Message ================================= <br>

then could you search if I have dream about animals? <br>
================================== Ai Message ================================== <br>
Tool Calls:
  retrieve_context_dreamjournal (call_dZj1UzAcaw53cJGvji0LCPGe)
 Call ID: call_dZj1UzAcaw53cJGvji0LCPGe
  Args:
    query: animals <br>
================================= Tool Message ================================= <br>
Name: retrieve_context_dreamjournal <br>

("Source: {'source': '/content/testdreamjournal2.txt'}\nContent: Dream 1: The Dog and the Bone\nDate: 12/05/2015\n\nI dream about a dog that gave me a bone.\n\n/end\n\nDream 2: The Floating Library\nDate: 03/18/2016\n\nI was in a giant library where all the books floated around me. When I opened one, I was pulled into the story itself. In one book, I was soaring through the clouds on the back of a golden eagle, feeling the wind rush past me.\n\n/end\n\nDream 3: Reverse City\nDate: 09/02/2016\n\nI walked through a city where everything was upside down. The roads were above my head, and people moved along the ceilings. When I touched certain objects, gravity flipped, and I fell upward instead of down.\n\n/end\n\nDream 4: Time-Travel Garden\nDate: 04/11/2017\n\nI wandered into a garden where each flower seemed to represent a different era. When I touched a rose, I found myself in ancient Rome, and a simple daisy sent me to a futuristic city full of glowing towers.\n\n/end\n\nDream 5: Ocean in the Sky\nDate: 08/27/2017\n\nI was swimming in a vast ocean suspended in the sky. Schools of glowing fish brushed past my face, and whales leapt gracefully from one cloud to another as the sunlight shimmered around me.\n\n/end\n\nDream 6: Endless Staircase\nDate: 01/19/2018\n\nI climbed a staircase that seemed to stretch on forever. Every landing transformed into something new—a dense jungle, a snowy mountain, a bustling marketplace—each more vivid than the last.\n\n/end\n\nDream 7: Mirror World\nDate: 06/05/2018\n\nI entered a room full of mirrors, but my reflections moved independently. One version of me waved and beckoned me into a parallel life where I had made different choices years ago.\n\n/end\n\nDream 8: Musical Forest\nDate: 10/22/2019\n\nI wandered through a forest where the trees hummed melodies and the flowers bloomed to the music. Every step I took changed the song, creating a kaleidoscope of color and sound around me.\n\n/end\n\nDream 9: Talking Animals City\nDate: 02/14/2020\n\nI found myself in a city where animals spoke my language. A fox ran a café, a raccoon drove a bus, and a wise old owl sold maps showing hidden secrets I had never known existed.\n\n/end\n\nDream 10: Vanishing Island\nDate: 07/30/2021\n\nI discovered an island that slowly dissolved into thin air. As it vanished, glowing bridges appeared, leading to new floating islands, each stranger and more beautiful than the one before.\n\n/end\n\nDream 11: Dream Market\nDate: 11/09/2022\n\nI wandered through a market where people traded memories, emotions, and fragments of dreams. I traded a memory of my happiest day for a dream where I was flying through a sky made entirely of candy-colored clouds.\n\n/end\n\nDream 12: Fire Phoenix Merge\nDate: 03/24/2026\n\nThe dream was about I was talking to someone and in the background, my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself.", [Document(id='a7663b69-c50d-46b4-b47e-82c26cca7e79', metadata={'source': '/content/testdreamjournal2.txt'}, page_content='Dream 1: The Dog and the Bone\nDate: 12/05/2015\n\nI dream about a dog that gave me a bone.\n\n/end\n\nDream 2: The Floating Library\nDate: 03/18/2016\n\nI was in a giant library where all the books floated around me. When I opened one, I was pulled into the story itself. In one book, I was soaring through the clouds on the back of a golden eagle, feeling the wind rush past me.\n\n/end\n\nDream 3: Reverse City\nDate: 09/02/2016\n\nI walked through a city where everything was upside down. The roads were above my head, and people moved along the ceilings. When I touched certain objects, gravity flipped, and I fell upward instead of down.\n\n/end\n\nDream 4: Time-Travel Garden\nDate: 04/11/2017\n\nI wandered into a garden where each flower seemed to represent a different era. When I touched a rose, I found myself in ancient Rome, and a simple daisy sent me to a futuristic city full of glowing towers.\n\n/end\n\nDream 5: Ocean in the Sky\nDate: 08/27/2017\n\nI was swimming in a vast ocean suspended in the sky. Schools of glowing fish brushed past my face, and whales leapt gracefully from one cloud to another as the sunlight shimmered around me.\n\n/end\n\nDream 6: Endless Staircase\nDate: 01/19/2018\n\nI climbed a staircase that seemed to stretch on forever. Every landing transformed into something new—a dense jungle, a snowy mountain, a bustling marketplace—each more vivid than the last.\n\n/end\n\nDream 7: Mirror World\nDate: 06/05/2018\n\nI entered a room full of mirrors, but my reflections moved independently. One version of me waved and beckoned me into a parallel life where I had made different choices years ago.\n\n/end\n\nDream 8: Musical Forest\nDate: 10/22/2019\n\nI wandered through a forest where the trees hummed melodies and the flowers bloomed to the music. Every step I took changed the song, creating a kaleidoscope of color and sound around me.\n\n/end\n\nDream 9: Talking Animals City\nDate: 02/14/2020\n\nI found myself in a city where animals spoke my language. A fox ran a café, a raccoon drove a bus, and a wise old owl sold maps showing hidden secrets I had never known existed.\n\n/end\n\nDream 10: Vanishing Island\nDate: 07/30/2021\n\nI discovered an island that slowly dissolved into thin air. As it vanished, glowing bridges appeared, leading to new floating islands, each stranger and more beautiful than the one before.\n\n/end\n\nDream 11: Dream Market\nDate: 11/09/2022\n\nI wandered through a market where people traded memories, emotions, and fragments of dreams. I traded a memory of my happiest day for a dream where I was flying through a sky made entirely of candy-colored clouds.\n\n/end\n\nDream 12: Fire Phoenix Merge\nDate: 03/24/2026\n\nThe dream was about I was talking to someone and in the background, my focus shifts to the forest in the background. Then a fire phoenix flies towards me and merges with myself.')]) <br>
================================== Ai Message ================================== <br>

Here are the dreams from your journal that involve animals: <br>

1. **Dream 1: The Dog and the Bone** (12/05/2015) <br>
   - You dreamt about a dog that gave you a bone. <br>

2. **Dream 2: The Floating Library** (03/18/2016) <br>
   - In the dream, you were soaring through the clouds on the back of a golden eagle while inside a floating library. <br>

3. **Dream 9: Talking Animals City** (02/14/2020) <br>
   - You found yourself in a city where animals spoke your language. A fox ran a café, a raccoon drove a bus, and a wise old owl sold maps showing hidden secrets. <br>

These dreams show a variety of interactions with different animals. If you'd like to discuss any of them further, feel free to ask! <br>



---

## LangSmith Studio Example tracing of above example 
![exampletracing-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/54dc1b13-3449-4d03-8bee-5b6202f4c0ed)



