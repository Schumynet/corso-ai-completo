# CORSO AI & AUTOMAZIONE
## Intelligenza Artificiale e OpenHands

---

## 📚 DESCRIZIONE DEL CORSO

Questo corso ti insegnerà come utilizzare l'intelligenza artificiale per automatizzare processi, creare agenti intelligenti e sviluppare applicazioni AI-powered.

**Durata stimata:** 60 ore
**Prerequisiti:** Basi di programmazione (corso precedente)

---

## 🎯 STRUTTURA DEL CORSO

### Parte 1: Fondamenti di Intelligenza Artificiale
- Modulo AI-1: Cos'è l'AI e come funziona
- Modulo AI-2: Large Language Models (LLM)
- Modulo AI-3: Prompt Engineering

### Parte 2: AI Agents
- Modulo AI-4: Cosa sono gli AI Agents
- Modulo AI-5: Strumenti e capacità degli agent
- Modulo AI-6: Progettazione di workflow

### Parte 3: OpenHands
- Modulo AI-7: Introduzione a OpenHands
- Modulo AI-8: Automazioni con OpenHands
- Modulo AI-9: Custom Script e integrazioni

### Parte 4: Progetti Pratici
- Modulo AI-10: Progetto - Assistant Personale AI
- Modulo AI-11: Progetto - Sistema di automazione completo
- Modulo AI-12: Progetto - AI Agent per business

---

## PARTE 1: FONDAMENTI DI INTELLIGENZA ARTIFICIALE

---

# MODULO AI-1: COS'È L'AI E COME FUNZIONA

## Lezione AI-1.1: Introduzione all'Intelligenza Artificiale

### Cos'è l'Intelligenza Artificiale?

L'**Intelligenza Artificiale (AI)** è la capacità di un computer di compiere attività che normalmente richiedono intelligenza umana. Queste includono:

- Comprensione del linguaggio naturale
- Riconoscimento di immagini
- Decisioni e ragionamento
- Apprendimento da esperienze
- Generazione di contenuti creativi

### Tipi di AI

#### AI Simbolica (Rule-based)
Sistemi che seguono regole predefinite. Esempi: sistemi esperti, algoritmi di ricerca.

```python
# Esempio di AI simbolica
def diagnostica(temperatura, tosse):
    if temperatura > 38 and tosse:
        return "Possibile influenza - consulta un medico"
    elif temperatura > 37 and tosse:
        return "Leggero raffreddore - riposo consigliato"
    elif tosse:
        return "Tosse secca - monitora i sintomi"
    else:
        return "Nessun sintomo preoccupante"
```

#### Machine Learning
Sistemi che apprendono pattern dai dati senza essere esplicitamente programmati.

```python
# Esempio concettuale di ML
# Il modello impara dai dati, non dalle regole fisse
# Training: dati_input → algoritmo → modello
# Inference: nuovo_dato → modello → predizione
```

#### Deep Learning
Subset del machine learning che usa reti neurali con molti strati (deep = profondo).

```
Input → [Layer 1] → [Layer 2] → [Layer 3] → ... → [Layer N] → Output
         (neuroni)   (neuroni)   (neuroni)       (neuroni)
```

### Breve Storia dell'AI

| Anno | Evento |
|------|--------|
| 1950 | Alan Turing propone il "Test di Turing" |
| 1956 | Nasce il termine "Artificial Intelligence" a Dartmouth |
| 1966 | ELIZA - primo chatbot (MIT) |
| 1997 | Deep Blue batte Kasparov a scacchi |
| 2011 | Watson vince Jeopardy |
| 2012 | AlexNet rivoluziona il deep learning (visione) |
| 2016 | AlphaGo batte il campione Go |
| 2020 | GPT-3 - primo LLM su larga scala |
| 2022 | ChatGPT - popolarizzazione conversazionale |
| 2023 | GPT-4, Claude, Gemini - multimodalità |
| 2024 | Agenti AI e automazione avanzata |

### AI debole vs AI forte

- **AI debole (Narrow AI)**: Specializzata in un task specifico. Es. Siri, Tesla Autopilot, GPT.
- **AI forte (General AI)**: Intelligenza generale pari a quella umana. Non esiste ancora.

### Applicazioni Pratiche dell'AI

| Settore | Applicazione |
|---------|-------------|
| Sanità | Diagnosi immagini mediche, scoperta farmaci |
| Finanza | Trading algoritmico, rilevamento frodi |
| Marketing | Personalizzazione, chatbot, raccomandazioni |
| Produzione | Quality control, manutenzione predittiva |
| Intrattenimento | Giochi, generazione contenuti, recommendation |
| Sviluppo | Code completion, bug detection, AI agents |

### Esercizio

1. Elenca 5 applicazioni AI che usi quotidianamente
2. Per ciascuna, identifica se è AI debole o forte
3. Pensa a un problema che potresti risolvere con l'AI

---

## Lezione AI-1.2: Come Funziona il Machine Learning

### Il Paradigma del Machine Learning

Nel ML tradizionale (programmazione):
```
PROGRAMMATORE → REGOLE + DATI → PROGRAMMA
```

Nel Machine Learning:
```
DATI + RISPOSTE ATTESE → ALGORITMO ML → MODELLO
NUOVI DATI + MODELLO → PREDIZIONI
```

### Tipi di Apprendimento

#### Supervised Learning (Apprendimento Supervisionato)
Il modello impara da dati etichettati (input → output corretto).

```python
# Esempio: classificazione email spam
# Training data
emails = [
    ("Vinci 1 milione!", "spam"),
    ("Riunione alle 15", "not_spam"),
    ("Offerta imperdibile", "spam"),
    ("Report mensile", "not_spam"),
]

# Il modello impara il pattern
# spam contiene parole come "vinci", "offerta"
# not_spam contiene parole come "riunione", "report"
```

#### Unsupervised Learning (Apprendimento Non Supervisionato)
Il modello trova pattern nei dati senza etichette.

```python
# Esempio: clustering di clienti
# Il modello raggruppa clienti simili senza sapere
# in anticipo quali gruppi esistono
# Gruppo 1: giovani, alta spesa
# Gruppo 2: anziani, bassa spesa
# Gruppo 3: famiglie, media spesa
```

#### Reinforcement Learning (Apprendimento per Rinforzo)
Il modello apprende attraverso tentativi ed errori, ricevendo ricompense o penalità.

```python
# Esempio: videogame AI
# Azione: muovi a destra
# Risultato: +10 punti (ricompensa!)
# Il modello impara che "destra" in questa situazione è buono
```

### Ciclo di Vita di un Progetto ML

```
1. Definizione Problema
   ↓
2. Raccolta Dati
   ↓
3. Preparazione Dati (Data Cleaning)
   ↓
4. Feature Engineering
   ↓
5. Training Modello
   ↓
6. Valutazione
   ↓
7. Deploy
   ↓
8. Monitoraggio e Aggiornamento
```

### Overfitting vs Underfitting

- **Overfitting**: Il modello "memorizza" i dati di training invece di imparare. Funziona male su dati nuovi.
- **Underfitting**: Il modello è troppo semplice per catturare i pattern. Funziona male anche su training.

```
Underfitting ←── IDEALE ──→ Overfitting

Semplicità modello
    bassa              alta
      ↑                  ↑
      |    *             |          *
      |       *          |       *
      |          *       |    **
      |             ****|******
      |                 |        *****
      └─────────────────┴─────────────────→
                   Complessità
```

### Metriche di Valutazione

```python
# Esempio per classificazione
# Accuracy: % di predizioni corrette
# Precision: % di positivi predetti che sono realmente positivi
# Recall: % di positivi reali identificati
# F1-Score: media armonica di precision e recall

y_true = [1, 0, 1, 1, 0, 1]
y_pred = [1, 0, 1, 0, 0, 1]

# Calcoli base
tp = sum(1 for t, p in zip(y_true, y_pred) if t == 1 and p == 1)  # True Positive
tn = sum(1 for t, p in zip(y_true, y_pred) if t == 0 and p == 0)  # True Negative
fp = sum(1 for t, p in zip(y_true, y_pred) if t == 0 and p == 1)  # False Positive
fn = sum(1 for t, p in zip(y_true, y_pred) if t == 1 and p == 0)  # False Negative

accuracy = (tp + tn) / len(y_true)  # 0.83
precision = tp / (tp + fp) if (tp + fp) > 0 else 0  # 0.80
recall = tp / (tp + fn) if (tp + fn) > 0 else 0     # 0.80
```

### Esercizio

1. Per ogni scenario, identifica il tipo di ML:
   - Rilevamento frodi su carta di credito
   - Raggruppare clienti per comportamento d'acquisto
   - GPT che genera testo
   - AI che impara a giocare a Minecraft

---

## Lezione AI-1.3: Reti Neurali e Deep Learning

### Il Neurone Artificiale

Un neurone artificiale riceve input, li combina con pesi, somma e applica una funzione di attivazione:

```
Input1 ──→ [w1] ─┐
Input2 ──→ [w2] ─┤
Input3 ──→ [w3] ─┴→ Σ + bias → activation → Output
```

```python
# Semplice neurone
def neurone(inputs, weights, bias, activation):
    # Somma pesata degli input
    z = sum(i * w for i, w in zip(inputs, weights)) + bias
    # Applica funzione di attivazione
    return activation(z)

# Esempio
inputs = [1.0, 0.5, 2.0]
weights = [0.2, 0.3, -0.1]
bias = 0.1

def relu(x):
    return max(0, x)

output = neurone(inputs, weights, bias, relu)
```

### Funzioni di Attivazione

```python
# ReLU (Rectified Linear Unit) - la più usata
relu(x) = max(0, x)

# Sigmoid - per probabilità (0-1)
import math
sigmoid(x) = 1 / (1 + math.exp(-x))

# Tangente Iperbolica - valori tra -1 e 1
tanh(x) = (e^x - e^(-x)) / (e^x + e^(-x))

# Softmax - per multi-class classification
def softmax(x):
    exp_x = [math.exp(i) for i in x]
    sum_exp = sum(exp_x)
    return [i / sum_exp for i in exp_x]
```

### Struttura di una Rete Neurale

```
INPUT LAYER     HIDDEN LAYERS      OUTPUT LAYER
(3 neuroni)    (4 neuroni)        (2 neuroni)

  ○ ──────────○ ──────────○         ○
  ○ ─────────○ ─────────○  ────   ○
  ○──────────○──────────○  ────   
              ○──────────○
              ○──────────○  ────   
```

### Deep Learning

"Deep" significa many hidden layers (da 3 a centinaia).

```python
# Con PyTorch
import torch
import torch.nn as nn

class ReteNeurale(nn.Module):
    def __init__(self):
        super().__init__()
        self.layers = nn.Sequential(
            nn.Linear(784, 256),    # Input → Hidden 1
            nn.ReLU(),              # Activation
            nn.Linear(256, 128),   # Hidden 1 → Hidden 2
            nn.ReLU(),              # Activation
            nn.Linear(128, 10),    # Hidden 2 → Output
            nn.Softmax(dim=1)       # Output
        )
    
    def forward(self, x):
        return self.layers(x)
```

### Convolutional Neural Networks (CNN)

Per elaborazione immagini. Rileva caratteristiche (features) a diversi livelli:

```
Immagine → Edge Detection → Texture → Pattern → Oggetto → Classe
           (strati bassi)   →      →    (strati alti)
```

### Recurrent Neural Networks (RNN)

Per dati sequenziali (testo, serie temporali). Hanno "memoria" del passato:

```
t1: "Ciao" → hidden_1
t2: "come" + hidden_1 → hidden_2  
t3: "stai" + hidden_2 → hidden_3 → output
```

### Transformer (la architettura dietro GPT, Claude, etc.)

Basati su **Self-Attention Mechanism** - il modello può "vedere" tutte le parti dell'input contemporaneamente.

```
Input: "Il gatto nero"
     ↓
Embedding + Positional Encoding
     ↓
Self-Attention (calcola relazioni tra tutti i token)
     ↓
Feed-Forward Network
     ↓
Output: Predizione prossimo token
```

### Esercizio

1. Disegna una rete neurale per classificare email (spam/not_spam) con:
   - Input layer per parole
   - 2 hidden layers
   - Output layer binario

2. Quale funzione di attivazione useresti per l'output di classificazione?

---

## Riepilogo Modulo AI-1

### Concetti Chiave
- L'AI include ML, deep learning, reti neurali
- ML impara da dati, non da regole esplicite
- Reti neurali profonde (deep learning) dominano many tasks
- Transformer sono l'architettura dietro GPT e Claude

### Prossima Lezione
Nel Modulo AI-2 affronteremo i Large Language Models (LLM) in dettaglio.