# MODULO AI-4: AI AGENTS

## Lezione AI-4.1: Cosa sono gli AI Agents

### Definizione

Un **AI Agent** è un sistema che usa un LLM per:
1. Comprendere obiettivi
2. Pianificare azioni
3. Usare strumenti (tools)
4. Compiere operazioni nel mondo reale
5. Iterare fino a completare l'obiettivo

### Agente vs Chatbot Tradizionale

| Aspetto | Chatbot Tradizionale | AI Agent |
|---------|--------------------| --------|
| Input | Testo | Testo, file, API, eventi |
| Output | Risposta testuale | Azioni concrete |
| Memoria | Solo conversazione attuale | Storico, contesto persistente |
| Strumenti | Nessuno | Può usarne molti |
| Autonomia | Nessuna | Può operare senza intervento |
| Iterazione | No | Sì, riprova se fallisce |

### Architettura di un AI Agent

```
┌─────────────────────────────────────────────────┐
│                    AGENT                          │
│                                                  │
│  ┌─────────────┐                                │
│  │    LLM      │ ← Il "cervello"               │
│  └─────────────┘                                │
│        ↓                                         │
│  ┌─────────────┐                                │
│  │  PLANNING   │ ← Decompone obiettivi         │
│  └─────────────┘                                │
│        ↓                                         │
│  ┌─────────────┐                                │
│  │   TOOLS     │ ← Capacità di azione          │
│  └─────────────┘                                │
│        ↓                                         │
│  ┌─────────────┐                                │
│  │   MEMORY    │ ← Conserva informazioni        │
│  └─────────────┘                                │
└─────────────────────────────────────────────────┘
```

### Componenti Chiave

#### 1. LLM Core
Il motore di ragionamento:
```python
# Esempio concettuale
response = llm.chat(
    messages=[{"role": "user", "content": prompt}]
)
```

#### 2. Planning
Scomposizione automatica in task:
```
Obiettivo: "Prenota volo Roma-Milano per domani"

↓
Piano:
1. Cerca voli Roma-Milano domani
2. Filtra per prezzo/orario preferiti
3. Verifica disponibilità
4. Prenota con dati carta
5. Invia conferma email
```

#### 3. Tool Use
Strumenti per interagire con il mondo:
```python
tools = [
    {
        "name": "search_flights",
        "description": "Cerca voli tra due città",
        "parameters": {"origin": str, "destination": str, "date": str}
    },
    {
        "name": "send_email",
        "description": "Invia email",
        "parameters": {"to": str, "subject": str, "body": str}
    },
    {
        "name": "read_file",
        "description": "Leggi contenuto file",
        "parameters": {"path": str}
    }
]
```

#### 4. Memory
Conservazione dello stato:
```python
# Short-term: conversazione attuale
short_term = conversation.messages

# Long-term: persistenza
long_term = {
    "user_preferences": {"budget": "medium", "airline": "Alitalia"},
    "past_interactions": [...],
    "learned_facts": {...}
}
```

### Framework Popolari per AI Agents

| Framework | Provider | Caratteristiche |
|-----------|----------| ---------------|
| LangChain | LangChain AI | Completo, molti integrations |
| LlamaIndex | LlamaIndex | Dati e retrieval |
| AutoGPT | Significant Gravitas | Agente autonomo |
| AutoGen | Microsoft | Multi-agent collaboration |
| CrewAI | CrewAI | Ruoli e collaborazione |

### Esempio con LangChain

```python
from langchain.agents import AgentExecutor, create_openai_functions_agent
from langchain_openai import ChatOpenAI
from langchain import hub

# Setup LLM
llm = ChatOpenAI(model="gpt-4-turbo")

# Definisci tools
tools = [search_web, read_file, write_file, send_email]

# Crea prompt dal hub
prompt = hub.pull("hwchase17/openai-functions-agent")

# Crea agent
agent = create_openai_functions_agent(llm, tools, prompt)

# Crea executor
agent_executor = AgentExecutor(agent=agent, tools=tools)

# Esegui
result = agent_executor.invoke({
    "input": "Cerca notizie su AI oggi e salvale in un file"
})
```

### Quando Usare gli AI Agents

✅ **Ideale per:**
- Task multi-step complessi
- Automazione di processi ripetitivi
- Ricerca e sintesi informazioni
- Assistenza personale

❌ **Non ideale per:**
- Task semplici one-shot
- Risposte rapide necessarie
- Alta precisione richiesta (es. medico/legale)

### Esercizio

1. Elenca 5 task che un AI Agent potrebbe compiere meglio di un chatbot
2. Per ogni task, identifica i tool necessari
3. Descrivi il planning per uno dei task

---

## Lezione AI-4.2: Tool Use e Capacità

### Cosa sono i Tools?

I **Tools** (strumenti) estendono le capacità dell'LLM permettendogli di:
- Cercare informazioni sul web
- Leggere e scrivere file
- Eseguire codice
- Interagire con API
- Controllare altri software

### Tool Calling

Il modello "decide" di usare un tool basandosi sul prompt:

```python
# Schema tool
tools = [{
    "name": "calcolatrice",
    "description": "Esegui calcoli matematici",
    "parameters": {
        "type": "object",
        "properties": {
            "expression": {
                "type": "string",
                "description": "Espressione matematica, es: 2+2*3"
            }
        },
        "required": ["expression"]
    }
}]

# Chiamata (simulata)
llm_response = {
    "tool_calls": [{
        "id": "call_123",
        "name": "calcolatrice",
        "arguments": {"expression": "2+2*3"}
    }]
}

# LLM vede l'output del tool
# e continua il ragionamento
```

### Tool Comuni

#### Web Search
```python
def search_web(query: str) -> str:
    """Cerca informazioni sul web"""
    results = google_search(query)
    return format_results(results)

# Output esempio
"""
1. Wikipedia - Intelligenza Artificiale
   L'intelligenza artificiale (IA) è l'abilità...
2. MIT Technology Review - AI News
   Latest developments in AI research...
"""
```

#### File System
```python
def read_file(path: str) -> str:
    """Leggi contenuto di un file"""
    with open(path, 'r') as f:
        return f.read()

def write_file(path: str, content: str) -> str:
    """Scrivi contenuto in un file"""
    with open(path, 'w') as f:
        f.write(content)
    return f"File {path} scritto con successo"
```

#### Code Execution
```python
def execute_code(code: str, language: str) -> str:
    """Esegui codice Python o altri linguaggi"""
    if language == "python":
        result = exec(code)  # in ambiente sicuro!
    return str(result)
```

#### API Calls
```python
def call_api(url: str, method: str = "GET", data: dict = None) -> str:
    """Chiama un'API REST"""
    response = requests.request(method, url, json=data)
    return response.text
```

### Creare Tools Personalizzati

```python
from langchain.tools import Tool
from langchain.chains import LLMMathChain
from langchain_community.utilities import WikipediaAPIWrapper

# Tool per cercare su Wikipedia
wiki = WikipediaAPIWrapper()
wiki_tool = Tool(
    name="Wikipedia",
    func=wiki.run,
    description="Cerca informazioni su Wikipedia"
)

# Tool per calcoli
llm_math = LLMMathChain(llm=llm)
math_tool = Tool(
    name="Calculator",
    func=llm_math.run,
    description="Esegui calcoli matematici"
)

# Aggrega tools
tools = [wiki_tool, math_tool, web_search_tool]
```

### Multi-Tool Workflow

```python
# Esempio: Ricerca, analizza e salva
task = "Trova le ultime notizie su AI e salvale in un report"

# Step 1: Ricerca
notizie = search_web("AI news today")

# Step 2: Analizza
analisi = llm.chat(f"""
Analizza queste notizie e riassumile in punti chiave:

{notizie}
""")

# Step 3: Salva
write_file("report_ai.md", analisi)
```

### Best Practices per Tools

```python
# ✅ Usa descrizioni chiare e dettagliate
good_tool = {
    "name": "get_weather",
    "description": """Ottieni il meteo per una città.
    Input: nome città (es: "Roma", "Milano")
    Output: temperatura, condizioni, umidità""",
    "parameters": {...}
}

# ❌ Descrizioni vaghe
bad_tool = {
    "name": "meteo",
    "description": "Dà il meteo"
}
```

### Error Handling nei Tools

```python
def robust_tool(param):
    try:
        result = risky_operation(param)
        return {"success": True, "data": result}
    except FileNotFoundError:
        return {"success": False, "error": "File non trovato"}
    except PermissionError:
        return {"success": False, "error": "Permesso negato"}
    except Exception as e:
        return {"success": False, "error": str(e)}
```

### Esercizio

1. Crea 3 tool personalizzati per un assistente di coding
2. Per ogni tool, scrivi descrizione e schema parametri
3. Implementa error handling per uno dei tool

---

## Lezione AI-4.3: Memory e State Management

### Tipi di Memoria

```
┌─────────────────────────────────────────────────────┐
│                   AGENT MEMORY                       │
│                                                      │
│  ┌──────────────────┐  ┌──────────────────┐        │
│  │   SHORT-TERM    │  │    LONG-TERM     │        │
│  │   (Context)     │  │   (Persistent)    │        │
│  │                 │  │                  │        │
│  │ • Conversazione │  │ • Preferenze     │        │
│  │ • Task attuale  │  │ • Storico       │        │
│  │ • Passi fatti   │  │ • Conoscenza    │        │
│  └──────────────────┘  └──────────────────┘        │
│                                                      │
│  ┌──────────────────┐  ┌──────────────────┐        │
│  │    WORKING       │  │     ENTITY       │        │
│  │    (Scratchpad)  │  │    (Knowledge)    │        │
│  │                 │  │                  │        │
│  │ • Calcoli       │  │ • Fatti utente   │        │
│  │ • Appunti       │  │ • Mappa concetti │        │
│  │ • tmp results   │  │ • Relationships  │        │
│  └──────────────────┘  └──────────────────┘        │
└─────────────────────────────────────────────────────┘
```

### Implementazione Base

```python
class SimpleAgentMemory:
    def __init__(self):
        self.messages = []      # Short-term
        self.persistent = {}     # Long-term
        self.scratchpad = {}    # Working memory
    
    def add_message(self, role, content):
        self.messages.append({"role": role, "content": content})
    
    def get_context(self, max_messages=10):
        """Ultimi N messaggi per il contesto"""
        return self.messages[-max_messages:]
    
    def set_fact(self, key, value):
        self.persistent[key] = value
    
    def get_fact(self, key, default=None):
        return self.persistent.get(key, default)
    
    def clear_short_term(self):
        self.messages = []
```

### Conversation Memory

```python
# LangChain ConversationBufferMemory
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory(
    memory_key="chat_history",
    return_messages=True,
    output_key="answer"
)

# Aggiungi interazione
memory.save_context(
    {"question": "Come stai?"},
    {"answer": "Bene, grazie!"}
)

# Recupera per il prossimo turno
chat_history = memory.load_memory_variables({})
```

### Persistent Memory con Database

```python
import sqlite3

class PersistentMemory:
    def __init__(self, db_path="memory.db"):
        self.conn = sqlite3.connect(db_path)
        self.create_tables()
    
    def create_tables(self):
        self.conn.execute("""
            CREATE TABLE IF NOT EXISTS facts (
                key TEXT PRIMARY KEY,
                value TEXT,
                updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
            )
        """)
    
    def save(self, key, value):
        self.conn.execute("""
            INSERT OR REPLACE INTO facts (key, value) VALUES (?, ?)
        """, (key, value))
        self.conn.commit()
    
    def recall(self, key):
        cursor = self.conn.execute(
            "SELECT value FROM facts WHERE key = ?", (key,)
        )
        result = cursor.fetchone()
        return result[0] if result else None
    
    def search(self, query):
        cursor = self.conn.execute(
            "SELECT * FROM facts WHERE value LIKE ?", (f"%{query}%",)
        )
        return cursor.fetchall()
```

### Entity Memory

```python
class EntityMemory:
    """Memorizza informazioni su entità specifiche"""
    
    def __init__(self):
        self.entities = {}  # nome -> {"facts": [], "last_mentioned": date}
    
    def add_entity(self, name, initial_facts=None):
        self.entities[name] = {
            "facts": initial_facts or [],
            "mentions": 0
        }
    
    def update_entity(self, name, new_fact):
        if name in self.entities:
            self.entities[name]["facts"].append(new_fact)
            self.entities[name]["mentions"] += 1
    
    def get_entity_info(self, name):
        return self.entities.get(name, {"facts": [], "mentions": 0})
```

### Summarization per Lunghi Contesti

```python
# Quando il contesto cresce troppo, riassumi
def summarize_if_needed(messages, llm, max_tokens=2000):
    total_tokens = estimate_tokens(messages)
    
    if total_tokens > max_tokens:
        # Estrai solo gli ultimi messaggi rilevanti
        recent = messages[-10:]
        
        # Chiedi al LLM di riassumere il resto
        summary_prompt = f"""
        Riassumi questa conversazione in punti chiave:
        
        {messages[:-10]}
        
        output: lista di fatti importanti da ricordare
        """
        
        summary = llm.predict(summary_prompt)
        return [summary] + recent
    
    return messages
```

### Esercizio

1. Implementa una classe SimpleAgentMemory con i tre tipi di memoria
2. Aggiungi un metodo per cercare fatti passati
3. Implementa la summarization per contesti lunghi

---

## Riepilogo Modulo AI-4

### Concetti Chiave
- AI Agents usano LLM + tools per compiere azioni concrete
- Components: LLM, planning, tools, memory
- Tool use estende le capacità del modello
- Memory management è cruciale per agent stateful

### Prossimo Modulo
Nel Modulo AI-5 affronteremo OpenHands in dettaglio - come creare automazioni concrete.