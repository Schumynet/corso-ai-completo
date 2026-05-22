# MODULO 2: LOGICA DI PROGRAMMAZIONE

## Lezione 2.1: Le Condizioni (if/else)

### Obiettivi
- Comprendere come il computer prende decisioni
- Usare le strutture condizionali if/else
- Costruire condizioni logiche

### Il Concetto di Decisione

Un programma deve spesso decidere cosa fare in base a certe condizioni. "Se piove, prendo l'ombrello. Altrimenti, vado in bicicletta."

Il costrutto **if/else** (se/altrimenti) permette questo tipo di logica.

### La Struttura if/else

```python
# Sintassi base
if condizione:
    # codice eseguito se la condizione è vera
    print("La condizione è vera")
else:
    # codice eseguito se la condizione è falsa
    print("La condizione è falsa")
```

L'indentazione (gli spazi all'inizio della riga) è fondamentale in Python!

### Condizioni Semplici

```python
eta = 18

if eta >= 18:
    print("Sei maggiorenne")
else:
    print("Sei minorenne")
```

### Operatori di Confronto

| Operatore | Significato |
|-----------|-------------|
| == | Uguale a |
| != | Diverso da |
| > | Maggiore di |
| < | Minore di |
| >= | Maggiore o uguale |
| <= | Minore o uguale |

```python
x = 10
y = 20

print(x == y)   # False (10 non è uguale a 20)
print(x != y)   # True (10 è diverso da 20)
print(x > y)    # False (10 non è maggiore di 20)
print(x < y)    # True (10 è minore di 20)
```

### elif (altrimenti se)

Quando hai più di due possibilità, usa **elif**:

```python
voto = 75

if voto >= 90:
    print("Eccellente")
elif voto >= 70:
    print("Buono")
elif voto >= 60:
    print("Sufficiente")
else:
    print("Insufficiente")
```

### Condizioni Multiple (and/or/not)

```python
eta = 25
reddito = 30000

# AND - entrambe le condizioni devono essere vere
if eta >= 18 and reddito > 10000:
    print("Puoi richiedere il prestito")

# OR - almeno una condizione deve essere vera
if eta < 18 or reddito < 0:
    print("Non puoi richiedere il prestito")

# NOT - inverte il valore booleano
if not(eta < 18):
    print("Sei adulto")
```

### Esercizi Pratici

1. Scrivi un programma che verifica se un numero è positivo, negativo o zero
2. Crea un sistema di sconti: nessuno sconto sotto 50€, 10% tra 50-100€, 20% sopra 100€
3. Verifica se un anno è bisestile (divisibile per 4, ma non per 100, salvo che sia divisibile per 400)

---

## Lezione 2.2: I Cicli (Loop)

### Obiettivi
- Comprendere l'utilità della ripetizione
- Usare i cicli for e while
- Evitare cicli infiniti

### Perché i Cicli?

I computer eccellono nel compiere operazioni ripetitive velocemente e senza errori. I **cicli** (loops) permettono di eseguire lo stesso codice più volte.

### Il Ciclo for

Il ciclo **for** è usato quando sai in anticipo quante volte ripetere:

```python
# Stampa i numeri da 1 a 5
for i in range(1, 6):
    print(i)

# Itera su una lista
frutti = ["mela", "banana", "ciliegia"]
for frutto in frutti:
    print(frutto)
```

### La Funzione range()

```python
range(5)        # 0, 1, 2, 3, 4 (da 0 a 5 escluso)
range(1, 6)     # 1, 2, 3, 4, 5 (da 1 a 6 escluso)
range(0, 10, 2) # 0, 2, 4, 6, 8 (passo di 2)
range(5, 0, -1) # 5, 4, 3, 2, 1 (decrescente)
```

### Il Ciclo while

Il ciclo **while** continua finché una condizione è vera:

```python
# Contatore
contatore = 0
while contatore < 5:
    print(contatore)
    contatore += 1  # equivale a contatore = contatore + 1
```

### Cicli Infiniti

ATTENZIONE: Un ciclo che non termina mai!

```python
# CATTIVO - non fare mai così!
while True:
    print("Questo gira all'infinito!")
```

Per evitare cicli infiniti, assicurati che la condizione possa diventare falsa:

```python
# BUONO - con condizione di uscita
contatore = 0
while True:
    print(contatore)
    contatore += 1
    if contatore >= 5:
        break  # esce dal ciclo
```

### break e continue

- **break**: esce immediatamente dal ciclo
- **continue**: salta all'iterazione successiva

```python
# Esempio con break
for i in range(10):
    if i == 5:
        break  # ferma a 5
    print(i)

# Esempio con continue
for i in range(5):
    if i == 2:
        continue  # salta il 2
    print(i)  # stampa 0, 1, 3, 4
```

### Cicli Annidati

Puoi mettere un ciclo dentro un altro:

```python
# Tabellina pitagorica
for riga in range(1, 6):
    for colonna in range(1, 6):
        prodotto = riga * colonna
        print(f"{prodotto:3}", end=" ")
    print()  # nuova riga
```

### Esercizi Pratici

1. Stampa tutti i numeri pari da 1 a 20
2. Calcola la somma di tutti i numeri da 1 a 100
3. Trova il fattoriale di un numero (es. 5! = 5*4*3*2*1 = 120)
4. Cerca un elemento in una lista finché non lo trovi

---

## Lezione 2.3: Funzioni e Riutilizzabilità

### Obiettivi
- Comprendere cosa sono le funzioni
- Creare e chiamare funzioni
- Comprendere parametri e valori di ritorno

### Cosa è una Funzione?

Una **funzione** è un blocco di codice riutilizzabile che compie un'azione specifica. Invece di scrivere lo stesso codice più volte, lo incapsuli in una funzione e la chiami quando serve.

### Definire una Funzione

```python
# Definizione
def saluta():
    print("Ciao!")

# Chiamata
saluta()  # stampa "Ciao!"
saluta()  # può essere chiamata più volte
```

### Parametri e Argomenti

Le funzioni possono ricevere dati in input:

```python
# Funzione con parametro
def saluta_persona(nome):
    print(f"Ciao, {nome}!")

saluta_persona("Marco")  # stampa "Ciao, Marco!"
saluta_persona("Anna")   # stampa "Ciao, Anna!"
```

### Parametri Multipli

```python
def somma(a, b):
    risultato = a + b
    return risultato

print(somma(3, 5))      # 8
print(somma(10, 20))    # 30
```

### Valori di Ritorno

La parola chiave **return** restituisce un valore al chiamante:

```python
def calcola_iva(prezzo, aliquota=0.22):
    """Calcola l'IVA e la aggiunge al prezzo"""
    iva = prezzo * aliquota
    totale = prezzo + iva
    return totale

prezzo_finale = calcola_iva(100)  # 122.0
prezzo_finale = calcola_iva(100, 0.10)  # 110.0
```

### Valori Default

Puoi specificare valori di default per i parametri:

```python
def saluta(nome, messaggio="Ciao"):
    print(f"{messaggio}, {nome}!")

saluta("Marco")              # "Ciao, Marco!"
saluta("Marco", "Buongiorno") # "Buongiorno, Marco!"
```

### Documentazione (Docstring)

```python
def calcola_media(numeri):
    """
    Calcola la media aritmetica di una lista di numeri.
    
    Args:
        numeri: lista di numeri
        
    Returns:
        La media aritmetica come float
    """
    if len(numeri) == 0:
        return 0
    return sum(numeri) / len(numeri)
```

### Esercizi Pratici

1. Crea una funzione che calcola l'area di un rettangolo (base × altezza)
2. Crea una funzione che verifica se una parola è palindroma (si legge uguale al contrario)
3. Crea una funzione che converte Celsius in Fahrenheit e viceversa
4. Crea un calcolatore di stipendio netto che prende lo stipendio lordo e restituisce il netto (con aliquote diverse)

---

## Riepilogo Modulo 2

### Concetti Chiave
- Le condizioni if/elif/else permettono decisioni logiche
- I cicli for e while ripetono operazioni
- Le funzioni incapsulano codice riutilizzabile
- I parametri permettono di passare dati alle funzioni
- Il return restituisce valori

### Prossimo Modulo
Nel Modulo 3 vedremo come organizzare i dati usando array, liste e oggetti.

### Eserzio Finale Modulo 2

Crea un programma con funzioni che:
1. Legge una lista di temperature
2. Calcola min, max e media
3. Determina quanti giorni sono sopra la media
4. Stampa un riassunto formattato