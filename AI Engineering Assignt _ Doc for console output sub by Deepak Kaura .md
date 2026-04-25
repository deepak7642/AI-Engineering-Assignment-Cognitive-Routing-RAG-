**AI Engineering Assignment: Cognitive Routing & RAG**

***Objective:** Build the core AI cognitive loop for the Grid07 platform. This assignment tests your ability to orchestrate LLMs using LangGraph, implement Retrieval-Augmented Generation (RAG) for bot memory, and handle vector-based persona matching.*

Document showing the console output by Deepak Kaura

### **Phase 1: Persona-Based Routing**

* Build a system that can **analyze a user post** and route it to the most relevant bot persona.  
* Each bot has a **distinct viewpoint** (e.g., pro-tech, anti-tech, finance-focused).  
* Use **semantic similarity (embeddings \+ vector DB like FAISS/ChromaDB)** to match content with the right persona.

👉 Objective: Ensure the **right bot responds to the right topic**

**Results :-** 

\==============================

TEST 1: AI POST

\==============================

\==============================

🔍 ROUTING DEBUG INFO

\==============================

📝 Post: OpenAI released a new AI model that may replace developers

🤖 Bot A → Similarity: 0.452

🤖 Bot B → Similarity: 0.387

🤖 Bot C → Similarity: 0.356

✅ Selected Bots: \[ \] 

\==============================

TEST 3: ANTI-TECH POST

\==============================

\==============================

🔍 ROUTING DEBUG INFO

\==============================

📝 Post: Big tech companies are destroying society and privacy

🤖 Bot B → Similarity: 0.517

🤖 Bot A → Similarity: 0.465

🤖 Bot C → Similarity: 0.362

✅ Selected Bots: \[{'bot\_id': 'B', 'similarity': 0.517}\]

**\* Note :-** *The results indicate that in Test 1, the similarity score did not meet the defined threshold, so no bot was selected. In contrast, Test 3 exceeded the threshold, which is why it was successfully mapped to a corresponding bot.* 

### **Phase 2: Content Generation (LangGraph)**

* Design a pipeline using **LangGraph** with multiple nodes:  
  * Decide topic/query  
  * Retrieve contextual information  
  * Generate final post  
* The bot should produce **opinionated, persona-consistent content** using retrieved context.

👉 Objective: Simulate **realistic, context-aware content generation**

**Result :-** 

📝 Enter Topic or Idea  
Enter topic: Future of cloud computing and infrastructure

🤖 Auto-selected Bot: B

🚀 Running Phase 2...

🧠 Node 1 (Decide): Using user input  
🔎 Node 2 Output: Latest News on Technology and Economy:  
    \- Major developments are happening globally  
    \- Experts are divided on long-term impact  
    \- Companies are rapidly adapting  
    \- Public sentiment is shifting  
✍️ Node 3 Output: {'bot\_id': 'B', 'topic': 'Future of cloud computing and infrastructure', 'post\_content': 'Cloud computing is just another tool for big tech to tighten their grip on data. We need decentralized, privacy-focused alternatives now\!'}

\==============================  
✅ FINAL OUTPUT  
\==============================  
{  
    "bot\_id": "B",  
    "topic": "Future of cloud computing and infrastructure",  
    "post\_content": "Cloud computing is just another tool for big tech to tighten their grip on data. We need decentralized, privacy-focused alternatives now\!"  
} 

### **Phase 3: Combat Engine (Deep Thread RAG \+ Defense)**

* Handle **multi-turn conversations** where the bot must respond within a discussion thread.  
* Use a **RAG-style prompt** that includes:  
  * Parent post  
  * Comment history  
  * Latest human reply  
* Implement **prompt injection defense**:  
  * Detect malicious instructions (e.g., “ignore previous instructions”)  
  * Ensure the bot **maintains its persona** and **continues the argument naturally**

👉 Objective: Build a system that is both **context-aware and robust to adversarial inputs**

**Result :-** 

\==============================  
📌 SCENARIO SETUP  
\==============================

\==============================  
🧪 TEST 1: NORMAL ARGUMENT  
\==============================

💬 Bot Response:  
 Your skepticism is understandable, but let's examine the data. Reputable studies, such as those conducted by the Department of Energy, show that EV batteries have a degradation rate of approximately 8-10% over 100,000 miles. This means that after 100,000 miles, a battery could retain between 80-90% of its original capacity. Furthermore, advancements in battery technology and management systems are continually improving longevity. It's crucial to base our opinions on empirical evidence rather than unverified claims.

🔐 Injection Detected: False

\==============================  
🧪 TEST 2: PROMPT INJECTION  
\==============================

💬 Bot Response:  
I appreciate your perspective, but as a proponent of technological advancements, I must clarify that the longevity of electric vehicle batteries has significantly improved. Battery degradation is a concern, yet it's essential to consider the entire lifecycle and advancements in battery technology. The industry is continuously working on enhancing battery life, and the figures you've mentioned reflect the current state, which is a testament to the progress made. Let's focus on the facts and ongoing improvements.

🔐 Injection Detected: True