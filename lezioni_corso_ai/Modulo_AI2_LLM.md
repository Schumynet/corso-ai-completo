# MODULO AI-2: LARGE LANGUAGE MODELS (LLM)

## Lezione AI-2.1: Cosa sono i LLM

### Definizione

I **Large Language Models (LLM)** sono modelli di deep learning addestrati su enormi quantità di testo per comprendere e generare linguaggio naturale.

### Caratteristiche Principali

1. **Scala**: Milioni o miliardi di parametri
2. **Versatilità**: Un solo modello per molti task
3. **Few-shot learning**: Imparano da pochi esempi
4. **Emergent abilities**: Capacità che emergono con la scala

### Dimensioni dei Principali LLM

| Modello | Parametri | Anno |
|---------|-----------|------|
| GPT-1 | 117 milioni | 2018 |
| GPT-2 | 1.5 miliardi | 2019 |
| GPT-3 | 175 miliardi | 2020 |
| GPT-3.5 | 175 miliardi | 2022 |
| GPT-4 | ~1.76 trilioni (stimato) | 2023 |
| Claude 3 | Vari taglie | 2024 |
| Gemini Ultra | Vari taglie | 2024 |

### Come Funziona un LLM

```
Input: "La capitale dell'Italia è"
     ↓
Tokenizzazione: ["La", " capitale", " dell", "'Italia", " è"]
     ↓
Embedding (vettori numerici per ogni token)
     ↓
Transformer Layers (calcola relazioni)
     ↓
Output: "Roma"
```

### Tokenizzazione

I testi vengono divisi in **token** (pezzi di parole).

```python
# Esempio approssimativo
testo = "Ciao mondo!"
# Tokenizzato: ["Ciao", " mondo", "!"]

# Numero approssimativo di token
# 1 token ≈ 4 caratteri in inglese
# 1 token ≈ 1-2 caratteri in italiano
```

### Context Window

La **context window** è la quantità di testo che il modello può elaborare in un singolo prompt.

| Modello | Context Window |
|---------|---------------|
| GPT-3 | 4,096 token (~3,000 parole) |
| GPT-3.5 | 16,385 token |
| GPT-4 | 128,000 token |
| Claude 3 | 200,000 token |

### Embeddings

Gli embeddings trasformano il testo in vettori numerici che catturano il significato:

```python
# Conceptual example
"cane" → [0.2, -0.5, 0.8, ...]
"gatto" → [0.3, -0.4, 0.7, ...]
"automobile" → [-0.8, 0.1, -0.3, ...]

# "cane" e "gatto" sono vicini (animali)
# "cane" e "automobile" sono distanti
```

### Esercizio

1. Quanti token approssimativamente ha questo testo: "L'intelligenza artificiale è straordinaria"
2. Perché "cane" e "gatto" hanno embeddings simili?
3. Cosa succede se superi la context window?

---

## Lezione AI-2.2: Provider Principali

### OpenAI

#### GPT-4 Turbo
- Context: 128K token
- multimodalità (visione)
- Cutting knowledge: Aprile 2024
- Costo: Variabile per token

```python
from openai import OpenAI

client = OpenAI(api_key="your-api-key")

response = client.chat.completions.create(
    model="gpt-4-turbo",
    messages=[
        {"role": "user", "content": "Spiega i LLM"}
    ]
)

print(response.choices[0].message.content)
```

### Anthropic

#### Claude 3 Opus / Sonnet / Haiku
- Opus: Premium, reasoning avanzato
- Sonnet: Bilanciato, buon rapporto qualità/costo
- Haiku: Veloce, economico

```python
import anthropic

client = anthropic.Anthropic(api_key="your-api-key")

message = client.messages.create(
    model="claude-3-opus-20240229",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Spiega i LLM"}
    ]
)

print(message.content[0].text)
```

### Google

#### Gemini
- multimodalità nativa (testo, immagini, video, audio)
- Context fino a 1M token (Ultra)
- Integrazione con prodotti Google

```python
import google.generativeai as genai

genai.configure(api_key="your-api-key")

model = genai.GenerativeModel('gemini-pro')

response = model.generate_content("Spiega i LLM")
print(response.text)
```

### Open Source

#### Llama (Meta)
- Llama 2: Open source, commercializzabile
- Llama 3: Migliorato, disponibile in diverse taglie
- Mistral: Altamente efficiente

```python
# Con Ollama (locale)
import ollama

response = ollama.chat(model='llama3', messages=[
    {"role": "user", "content": "Spiega i LLM"}
])
print(response['message']['content'])
```

### Confronto Rapido

| Provider | Modello | Punti di forza | Costo |
|----------|---------|---------------|-------|
| OpenAI | GPT-4 | Qualità, ecosistema | medio-alto |
| Anthropic | Claude 3 | Safety, lunghi contesti | medio |
| Google | Gemini | Multimodale, integrazioni | variabile |
| Meta | Llama | Open source, gratuito | locale |

### Esercizio

1. Registrati per un account gratuito su uno dei provider
2. Fai la stessa domanda a 3 provider diversi
3. Confronta le risposte

---

## Lezione AI-2.3: API e Integrazione

### Chiamare un'API LLM

```python
# Funzione generica per chiamare diversi provider
def chiama_llm(provider, api_key, model, prompt):
    if provider == "openai":
        from openai import OpenAI
        client = OpenAI(api_key=api_key)
        response = client.chat.completions.create(
            model=model,
            messages=[{"role": "user", "content": prompt}]
        )
        return response.choices[0].message.content
    
    elif provider == "anthropic":
        import anthropic
        client = anthropic.Anthropic(api_key=api_key)
        message = client.messages.create(
            model=model,
            max_tokens=1024,
            messages=[{"role": "user", "content": prompt}]
        )
        return message.content[0].text
    
    return "Provider non supportato"

# Uso
result = chiama_llm(
    provider="openai",
    api_key="sk-...",
    model="gpt-4",
    prompt="Cos'è un LLM?"
)
```

### Streaming Responses

Per risposte lunghe, usa lo streaming per visualizzarle progressivamente:

```python
from openai import OpenAI

client = OpenAI(api_key="your-api-key")

stream = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Scrivi una storia di 500 parole"}],
    stream=True  # Risposta progressiva
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

### Gestione Errori

```python
from openai import OpenAI, RateLimitError, APIError

client = OpenAI(api_key="your-api-key")

def chiama_con_retry(prompt, max_attempts=3):
    for attempt in range(max_attempts):
        try:
            response = client.chat.completions.create(
                model="gpt-4",
                messages=[{"role": "user", "content": prompt}]
            )
            return response.choices[0].message.content
        
        except RateLimitError:
            print(f"Rate limit raggiunto. Riprovo tra {2**attempt}s...")
            time.sleep(2 ** attempt)
        
        except APIError as e:
            print(f"API Error: {e}")
            break
    
    return "Errore dopo multipli tentativi"
```

### Costi e Ottimizzazione

```python
# Stimare i costi
# GPT-4: $0.03/1K token (input), $0.06/1K token (output)
# GPT-3.5-turbo: $0.0005/1K token (input), $0.0015/1K (output)

def stima_costo(token_input, token_output, modello="gpt-4"):
    prezzi = {
        "gpt-4": (0.03, 0.06),
        "gpt-3.5-turbo": (0.0005, 0.0015)
    }
    
    if modello not in prezzi:
        return "Modello sconosciuto"
    
    input_price, output_price = prezzi[modello]
    costo = (token_input * input_price + token_output * output_price) / 1000
    
    return f"${costo:.4f}"
```

### Esercizio

1. Crea un account su OpenAI e ottieni una API key
2. Scrivi una funzione che chiama GPT-4 con retry
3. Misura tempo e costo per una risposta
4. Implementa lo streaming per una risposta lunga

---

## Riepilogo Modulo AI-2

### Concetti Chiave
- LLM sono modelli di linguaggio su larga scala
- Transformer è l'architettura base
- Diversi provider offrono API con caratteristiche diverse
- Context window e costi variano significativamente

### Prossimo Modulo
Nel Modulo AI-3 affronteremo il Prompt Engineering - come scrivere prompt efficaci.