# MODULO AI-3: PROMPT ENGINEERING

## Lezione AI-3.1: Fondamenti del Prompt Engineering

### Cos'è il Prompt Engineering?

Il **Prompt Engineering** è l'arte e la scienza di scrivere prompt efficaci per ottenere risposte desiderate dai LLM.

Un buon prompt è:
- **Chiaro**: l'LLM capisce esattamente cosa vuoi
- **Specifico**: fornisce dettagli e contesto
- **Strutturato**: organizzato in modo logico
- **Completo**: include tutto il necessario per rispondere

### Struttura Base di un Prompt

```
1. CONTESTO / INFORMAZIONI DI BASE
   (Background necessario per capire)
   ↓
2. ISTRUZIONE / AZIONE
   (Cosa devi fare)
   ↓
3. FORMATO / VINCOLI
   (Come devi rispondere)
   ↓
4. ESEMPI (opzionali)
   (Few-shot examples)
```

### Esempio Base

```python
# ❌ Cattivo prompt (vago)
prompt = "Scrivi qualcosa sui cani"

# ✅ Buon prompt (chiaro e specifico)
prompt = """
Scrivi un articolo di blog di 500 parole sui golden retriever.

L'articolo deve:
- Avere un titolo accattivante
- Includere informazioni su:
  * Temperamento e personalità
  * Cure e mantenimento
  * Addestramento consigliato
- Essere scritto in tono amichevole
- Concludere con una call-to-action

Pubblico target: famiglie che cercano un cane
"""
```

### Livelli di Dettaglio

```python
# Livello 1: Minimale
prompt = "Traduci in inglese: Ciao come stai?"

# Livello 2: Con contesto
prompt = """
Traduci la seguente frase dall'italiano all'inglese americano colloquiale.

Frase: Ciao come stai?

Note:
- Mantieni il tono informale
- Usa espressioni naturali
"""

# Livello 3: Completo con esempi
prompt = """
Sei un traduttore professionista italiano-inglese.
Traduci in modo naturale e colloquiale.

REGOLE:
1. Mantieni il tono originale
2. Usa espressioni idiomatiche
3. Adatta i proverbi se necessario

ESEMPIO:
Input: "Non è tutto oro quel che luccica"
Output: "All that glitters is not gold"

ORA TRADUCI:
Input: "Ciao come stai?"
Output:"""
```

### Principi Fondamentali

1. **Sii esplicito**: Non dare per scontato nulla
2. **Spezzetta i task complessi**: Un passo alla volta
3. **Dai ruoli**: "Sei un esperto chef italiano"
4. **Usa delimitatori**: Separa chiaramente le parti
5. **Richiedi il formato**: Dichiara come vuoi la risposta

### Esercizio

1. Riscrivi questi prompt in modo migliore:
   - "Aiutami"
   - "Scrivi codice Python"
   - "Spiega l'universo"

2. Per ogni prompt migliorato, spiega cosa hai aggiunto

---

## Lezione AI-3.2: Tecniche Avanzate

### Few-Shot Learning

Dare esempi nella conversazione per guidare il modello:

```python
# Zero-shot (senza esempi)
prompt = """
Classifica il sentiment come POSITIVO, NEGATIVO o NEUTRO:
"Questo prodotto è ok"
"""

# Few-shot (con esempi)
prompt = """
Classifica il sentiment come POSITIVO, NEGATIVO o NEUTRO:

Esempi:
"Adoro questo prodotto!" → POSITIVO
"Non mi piace per niente" → NEGATIVO
"Funziona, fa il suo lavoro" → NEUTRO

Classifica:
"Questo prodotto è ok"
"""
```

### Chain of Thought (CoT)

Incoraggia il ragionamento passo-passo:

```python
# Senza CoT
prompt = """
Se Mario ha 3 mele e ne compra 5, quante mele ha in tutto?
"""

# Con CoT
prompt = """
Risolvi il problema passo passo.

Problema: Se Mario ha 3 mele e ne compra 5, quante mele ha in tutto?

Ragionamento:
1. Mario parte con 3 mele
2. Aggiunge 5 mele
3. Totale: 3 + 5 = 8 mele

Risposta:"""
```

### Zero-Shot CoT

Chiedi semplicemente di pensare:

```python
prompt = """
Problema: Se un treno viaggia a 100 km/h per 2 ore, quanti km percorre?

Rispondi pensando passo passo.
"""
```

### Tree of Thoughts (ToT)

Esplora multiple vie di ragionamento:

```python
prompt = """
Stai risolvendo un problema di ottimizzazione per un e-commerce.

Opzione A: Discount del 20% per tutti
  - Pro: Attrae clienti
  - Contro: Margini bassi

Opzione B: Free shipping sopra i 50€
  - Pro: Aumenta carrello medio
  - Contro: Costi spedizione

Opzione C: Bundle sconto
  - Pro: Vendite multiple
  - Contro: Complessità

Analizza ogni opzione considerando:
- Impatto sui ricavi
- Costi operativi
- Esperienza cliente

Quale raccomandi e perché?"""
```

### Role Prompting

Assegna un'identità specifica:

```python
prompt = """
Sei Marco, un coach di vita con 20 anni di esperienza.
Il tuo stile è empatico ma diretto.
Parli in modo ispirazionale ma realistico.

Una persona ti dice: "Non so cosa fare della mia vita"

Rispondi come Marco farebbe, in 2-3 paragrafi.
"""
```

### System vs User vs Assistant

```python
# System: istruzioni generali (una volta, all'inizio)
system = """
Sei un assistente finanziario esperto.
Rispondi solo a domande di finanza personale.
Se ti chiedono altro, dillo gentilmente.
"""

# User: la domanda dell'utente
user = "Come investire 10.000 euro?"

# Assistant: risposta del modello (in chat, per contesto)
assistant = "Per investire 10.000 euro..."

# In pratica con l'API:
messages = [
    {"role": "system", "content": system},
    {"role": "user", "content": user}
]
```

### Structured Output

Chiedi output in un formato specifico:

```python
prompt = """
Analizza il seguente testo e restituisci un JSON.

Testo: "La pizza margherita è inventata nel 1889 da Raffaele Esposito 
a Napoli in onore della regina Margherita."

Output JSON richiesto:
{
  "titolo": (stringa),
  "data": (stringa o null),
  "luogo": (stringa),
  "personaggi": [lista di nomi],
  "categoria": "storia" o "cibo" o "altro",
  "riassunto": (stringa massimo 50 parole)
}
"""
```

### Esercizio

1. Scrivi un prompt per un avvocato AI che risponde solo a domande legali
2. Usa CoT per risolvere: "Se 5 macchine producono 50 pezzi in 2 ore, quanti pezzi producono 8 macchine in 3 ore?"
3. Crea un prompt per generare ricette con structured output JSON

---

## Lezione AI-3.3: Patterns e Best Practices

### Pattern Comuni

#### 1. Query Expansion
Scomponi domande complesse in sotto-domande:

```python
prompt = """
Domanda: Quali sono i pro e contro di comprare vs affittare casa?

Scomponi in:
1. Vantaggi acquisto
2. Svantaggi acquisto
3. Vantaggi affitto
4. Svantaggi affitto
5. Fattori da considerare (età, reddito, località)

Per ogni punto, dai 2-3 argomenti specifici.
"""
```

#### 2. Persona-Matching
Adatta il tono al pubblico target:

```python
# Per bambini
prompt = """
Spiega il sistema solare a un bambino di 8 anni.
Usa parole semplici, analogie con cose che conosce.
Massimo 100 parole.
"""

# Per tecnici
prompt = """
Spiega il sistema solare includendo:
- Composizione dei pianeti
- Leggi di Keplero
- Transfer orbitale

Usa termini tecnici appropriati.
"""
```

#### 3. Constraint Refinement
Aggiungi vincoli progressivamente:

```python
prompt = """
Scrivi un tweet (280 caratteri) sul remote working.

Prima bozza:
[scrivi qui]

Ora raffina seguendo:
- Deve essere engaging (curiosità o umorismo)
- Include un dato o statistica
- Ha call-to-action implicito

Tweet finale:"""
```

### Debug di Prompt

Quando il prompt non funziona:

```python
# Checklist
checklist = """
□ Il modello ha capito il task? (chiedi di ripetere)
□ Manca contesto? (aggiungi informazioni)
□ Il formato è chiaro? (esempio di output)
□ Ci sono ambiguità? (specifica meglio)
□ Hai usato delimitatori? (### per sezioni)
□ Hai dato esempi? (few-shot se necessario)
"""

# Test sistematico
test_prompts = [
    "versione minima",
    "versione con contesto",
    "versione con esempi",
    "versione con CoT"
]
```

### Common Mistakes

```python
# ❌ Troppo vago
prompt = "Parlami di Python"

# ✅ Specifico
prompt = """
Spiega la differenza tra list e tuple in Python.
Per ogni differenza, dammi un esempio di quando usare l'una o l'altra.
Conclusione pratica su quando scegliere quale.
"""

# ❌ Contraddizioni nel prompt
prompt = """
Scrivi un testo lungo E anche breve
"""

# ✅ Univoco
prompt = """
Scrivi un testo di massimo 300 parole
"""

# ❌ Assunzioni non esplicite
prompt = """
Traduci: "How are you?"
"""

# ✅ Con contesto
prompt = """
Traduci dall'inglese all'italiano, tono informale:
"How are you?"

Nota: È un saluto iniziale tra amici italiani.
"""
```

### Template Riutilizzabili

```python
# Template per spiegazioni
TEMPLATE_SPIEGAZIONE = """
Argomento: {argomento}

Livello: {livello} (base/intermedio/avanzato)

Struttura richiesta:
1. Definizione breve (1 frase)
2. Spiegazione principale (2-3 paragrafi)
3. Esempio pratico (codice o caso d'uso)
4. Errori comuni da evitare
5. Risorse per approfondire

Argomento: {insert_argomento}
Livello: {insert_livello}
"""

# Template per codice
TEMPLATE_CODICE = """
Sei un developer esperto in {linguaggio}.

Contesto: {contesto}

Requisiti:
- {requisito1}
- {requisito2}

Vincoli:
- {vincolo1}
- {vincolo2}

Output richiesto:
1. Breve spiegazione dell'approccio
2. Codice completo e commentato
3. Note su possibili errori
"""
```

### Esercizio Finale

Crea un prompt per ciascuno:
1. Assistente per prenotare appuntamenti
2. Revisore di codice che spiega i problemi
3. Generatore di nomi per startup (3 opzioni con rationale)
4. Tutore di lingue che corregge e spiega errori

---

## Riepilogo Modulo AI-3

### Concetti Chiave
- Prompt engineering è fondamentale per ottenere risultati
- Struttura: contesto + istruzione + formato + esempi
- Few-shot, CoT, role prompting sono tecniche potenti
- Testa e raffina i prompt sistematicamente

### Prossimo Modulo
Nel Modulo AI-4 affronteremo gli AI Agents - sistemi che usano LLM per compiere azioni.