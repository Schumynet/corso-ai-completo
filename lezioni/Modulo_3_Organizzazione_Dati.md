# MODULO 3: ORGANIZZAZIONE DEI DATI

## Lezione 3.1: Array e Liste

### Obiettivi
- Comprendere cosa sono array e liste
- Manipolare collezioni di elementi
- Usare metodi comuni delle liste

### Cosa sono le Liste?

Una **lista** (list) è una collezione ordinata di elementi. Puoi pensarla come una fila di scatole, ognuna con un numero (indice) e un contenuto.

```python
# Creare una lista
frutti = ["mela", "banana", "ciliegia", "durian"]

# Accedere agli elementi (gli indici partono da 0!)
print(frutti[0])   # "mela"
print(frutti[1])   # "banana"
print(frutti[-1])  # "durian" (ultimo elemento)
```

### Slicing (Fette)

```python
numeri = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

numeri[2:5]    # [2, 3, 4] - dal 2 al 4 (5 escluso)
numeri[:5]     # [0, 1, 2, 3, 4] - dall'inizio al 4
numeri[5:]     # [5, 6, 7, 8, 9] - dal 5 alla fine
numeri[::2]    # [0, 2, 4, 6, 8] - uno sì, uno no
numeri[::-1]   # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] - al contrario
```

### Modificare le Liste

```python
lista = [1, 2, 3]

# Aggiungere elementi
lista.append(4)      # [1, 2, 3, 4] - aggiunge alla fine
lista.insert(0, 0)   # [0, 1, 2, 3, 4] - inserisce in posizione
lista.extend([5, 6]) # [0, 1, 2, 3, 4, 5, 6] - aggiunge una lista

# Rimuovere elementi
lista.pop()          # rimuove l'ultimo: [0, 1, 2, 3, 4, 5]
lista.pop(0)         # rimuove l'elemento in posizione 0
lista.remove(3)       # rimuove il primo 3 trovato

# Ordinare
numeri = [3, 1, 4, 1, 5, 9, 2, 6]
numeri.sort()         # [1, 1, 2, 3, 4, 5, 6, 9]
numeri.sort(reverse=True)  # [9, 6, 5, 4, 3, 2, 1, 1]
```

### List Comprehensions

Modo conciso per creare liste:

```python
# Tradizionale
quadrati = []
for x in range(10):
    quadrati.append(x ** 2)

# Con list comprehension
quadrati = [x ** 2 for x in range(10)]

# Con condizione
pari = [x for x in range(20) if x % 2 == 0]  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

### Array vs Liste

In Python, le liste sono la struttura dati principale. Gli **array** (dal modulo `array`) sono più efficienti per grandi quantità di dati numerici dello stesso tipo.

```python
from array import array

# Array di interi (più efficiente in memoria)
numeri = array('i', [1, 2, 3, 4, 5])
```

### Esercizi Pratici

1. Crea una lista dei tuoi film preferiti e stampa il primo, l'ultimo e il secondo
2. Data una lista di numeri, filtra solo i positivi
3. Data una lista di nomi, crea una nuova lista con i nomi in maiuscolo
4. Rovescia una lista senza usare reverse()

---

## Lezione 3.2: Oggetti e Strutture

### Obiettivi
- Comprendere cosa sono gli oggetti
- Creare e usare dizionari
- Lavorare con strutture dati complesse

### I Dizionari

Un **dizionario** (dictionary) è una collezione di coppie chiave-valore. Ogni elemento ha una chiave univoca che permette un accesso rapido.

```python
# Creare un dizionario
persona = {
    "nome": "Marco",
    "cognome": "Rossi",
    "età": 30,
    "città": "Roma"
}

# Accedere ai valori
print(persona["nome"])      # "Marco"
print(persona.get("età"))   # 30

# Usare get con default
print(persona.get("telefono", "Non specificato"))  # "Non specificato"
```

### Modificare Dizionari

```python
persona = {"nome": "Marco", "età": 30}

# Aggiungere/modificare
persona["città"] = "Milano"    # aggiunge
persona["età"] = 31            # modifica

# Rimuovere
del persona["città"]           # cancella
eta = persona.pop("età")      # rimuove e restituisce

# Verificare esistenza chiave
if "nome" in persona:
    print(persona["nome"])
```

### Dizionari Annidati

```python
utente = {
    "anagrafica": {
        "nome": "Marco",
        "cognome": "Rossi"
    },
    "contatti": {
        "email": "marco@email.com",
        "telefono": "3331234567"
    },
    "attivo": True
}

# Accesso annidato
print(utente["anagrafica"]["nome"])           # "Marco"
print(utente["contatti"]["email"])           # "marco@email.com"
```

### Iterare sui Dizionari

```python
persona = {"nome": "Marco", "età": 30, "città": "Roma"}

# Solo chiavi
for chiave in persona:
    print(chiave)

# Solo valori
for valore in persona.values():
    print(valore)

# Chiavi e valori insieme
for chiave, valore in persona.items():
    print(f"{chiave}: {valore}")
```

### Oggetti in Python (Classi)

Gli **oggetti** sono istanze di **classi**. Una classe definisce la struttura (attributi) e il comportamento (metodi).

```python
class Persona:
    def __init__(self, nome, cognome, età):
        # Attributi
        self.nome = nome
        self.cognome = cognome
        self.età = età
    
    # Metodo
    def presentati(self):
        return f"Ciao, sono {self.nome} {self.cognome}"
    
    def è_maggiorenne(self):
        return self.età >= 18

# Creare un'istanza
marco = Persona("Marco", "Rossi", 30)

# Usare i metodi
print(marco.presentati())     # "Ciao, sono Marco Rossi"
print(marco.è_maggiorenne()) # True
```

### Esercizi Pratici

1. Crea un dizionario per un libro con titolo, autore, anno, ISBN
2. Crea una lista di dizionari per rappresentare una rubrica (5 contatti)
3. Cerca un contatto per nome nella rubrica
4. Crea una classe `Cerchio` con attributo raggio e metodi per area e circonferenza

---

## Lezione 3.3: JSON - Il Formato Universale

### Obiettivi
- Comprendere cosa è JSON
- Leggere e scrivere file JSON
- Convertire tra Python e JSON

### Cos'è JSON?

**JSON** (JavaScript Object Notation) è un formato standard per scambiare dati tra sistemi diversi. È leggibile dagli umani e facile da elaborare per i computer.

```json
{
    "nome": "Marco",
    "età": 30,
    "hobby": ["leggere", "nuoto", "viaggi"],
    "indirizzo": {
        "via": "Roma 123",
        "città": "Milano"
    },
    "attivo": true
}
```

### JSON in Python

```python
import json

# Dizionario Python
persona = {
    "nome": "Marco",
    "età": 30,
    "hobby": ["leggere", "nuoto"]
}

# Convertire Python → JSON (serializzazione)
json_string = json.dumps(persona, indent=2)
print(json_string)

# Convertire JSON → Python (deserializzazione)
persona_dict = json.loads(json_string)
print(persona_dict["nome"])  # "Marco"
```

### Leggere e Scrivere File JSON

```python
import json

# Scrivi su file
dati = {"nome": "Marco", "punteggio": 95}
with open("dati.json", "w") as f:
    json.dump(dati, f, indent=2)

# Leggi da file
with open("dati.json", "r") as f:
    dati_caricati = json.load(f)
print(dati_caricati)
```

### JSON con Date e Tipi Personalizzati

```python
import json
from datetime import datetime

# json.dumps non gestisce datetime di default
dati = {
    "nome": "Marco",
    "data": datetime.now()  # oggetto datetime
}

# Soluzione 1: convertire in stringa
dati["data"] = dati["data"].isoformat()
json_string = json.dumps(dati)

# Soluzione 2: usare un custom encoder
class DateEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, datetime):
            return obj.isoformat()
        return super().default(obj)

json_string = json.dumps(dati, cls=DateEncoder)
```

### API e JSON

Le API REST restituiscono dati in formato JSON:

```python
import requests
import json

# Chiamare un'API
risposta = requests.get("https://api.github.com/users/Schumynet")
dati = risposta.json()

# Accedere ai dati
print(f"Nome: {dati['login']}")
print(f"Repos: {dati['public_repos']}")
```

### Esercizi Pratici

1. Crea un file JSON con 5 prodotti (nome, prezzo, quantità)
2. Leggi il file e calcola il valore totale del magazzino
3. Aggiungi un nuovo prodotto e salva
4. Filtra i prodotti con quantità inferiore a 10

---

## Riepilogo Modulo 3

### Concetti Chiave
- Le liste memorizzano elementi ordinati accessibili per indice
- I dizionari memorizzano coppie chiave-valore
- Gli oggetti (classi) combinano dati e comportamento
- JSON è il formato standard per scambiare dati tra sistemi

### Prossimo Modulo
Nel Modulo 4 scoprirai come funziona il web: client, server, API e HTTP.

### Eserzio Finale Modulo 3

Crea un sistema di gestione studenti:
1. Ogni studente ha nome, voti (lista), media
2. Salva i dati in un file JSON
3. Leggi i dati e mostra la classifica per media
4. Trova lo studente migliore e quello con voti più bassi