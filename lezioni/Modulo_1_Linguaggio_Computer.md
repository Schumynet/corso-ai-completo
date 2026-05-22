# MODULO 1: IL LINGUAGGIO DEL COMPUTER

## Lezione 1.1: Come Pensa un Computer

### Obiettivi
- Comprendere la differenza tra hardware e software
- Capire come i computer elaborano le informazioni
- Riconoscere il concetto di istruzioni precise

### Contenuto

Il computer è una macchina straordinariamente stupida ma velocissima. Non ha intelligenza propria, non capisce il significato delle parole, non ha opinioni o emozioni. Un computer fa esattamente quello che gli viene detto di fare, niente di più, niente di meno.

#### Il Concetto di Istruzioni

Immagina di dare istruzioni a un机器人 nuovo che non sa fare nulla. Se gli dici "fammi un caffè", probabilmente non saprebbe da dove iniziare. Ma se gli scrivi passo dopo passo:

1. Vai in cucina
2. Apri l'armadietto sopra il lavello
3. Prendi il barattolo del caffè
4. Apri il barattolo
5. Prendi un cucchiaino
6. Metti due cucchiaini di caffè nella tazza
7. ...e così via

Un computer funziona esattamente così. Ha bisogno di istruzioni precise, complete, in un ordine logico.

#### Bit e Byte

Tutto nel computer si riduce a due stati: acceso e spento, rappresentati da 1 e 0. Un singolo 0 o 1 si chiama **bit** (binary digit). Otto bit insieme formano un **byte**.

```
0 = OFF (spento)
1 = ON (acceso)

Byte esempio: 01000001 = rappresenta la lettera "A"
```

Con un byte possiamo rappresentare 256 valori diversi (da 0 a 255). Con due byte (16 bit) ne abbiamo 65.536.

#### Perché è Importante?

Capire che il computer lavora con 0 e 1 ti aiuta a comprendere:
- Perché i file hanno dimensioni specifiche
- Perché ci sono limiti tecnici
- Perché alcuni calcoli sono imprecisi

### Esercizio Pratico

Prova a scrivere le istruzioni dettagliate per un'attività quotidiana come "prepararti per uscire di casa". Suddividi ogni azione in passi microscopici. Questo esercizio ti abitua al pensiero sistematico necessario per programmare.

---

## Lezione 1.2: Dal Codice Sorgente all'Esecuzione

### Obiettivi
- Comprendere cosa è il codice sorgente
- Distinguere tra compilatori e interpreti
- Conoscere il ciclo sviluppo-esecuzione

### Il Codice Sorgente

Il **codice sorgente** (source code) è l'insieme di istruzioni scritte in un linguaggio di programmazione. È leggibile dagli esseri umani, scritto in file di testo.

Esempio di codice Python:
```python
print("Ciao, mondo!")
```

Esempio di codice JavaScript:
```javascript
console.log("Ciao, mondo!");
```

### Compilatori vs Interpreti

#### Compilatore
Il compilatore traduce tutto il codice in anticipo in istruzioni macchina (codice oggetto). Il file risultante può essere eseguito direttamente senza il compilatore.

Linguaggi compilati: C, C++, Go, Rust

```
Codice Sorgente → [Compilatore] → File Eseguibile
```

#### Interprete
L'interprete traduce ed esegue il codice riga per riga, ogni volta che il programma viene eseguito.

Linguaggi interpretati: Python, JavaScript, Ruby, PHP

```
Codice Sorgente → [Interprete] → (traduzione ed esecuzione riga per riga)
```

### Bytecode e Virtual Machines

Java e C# usano un approccio ibrido: il codice viene compilato in **bytecode**, un formato intermedio che viene poi eseguito da una **virtual machine** (JVM, CLR).

```
Codice Sorgente → [Compilatore] → Bytecode → [VM] → Esecuzione
```

### Ciclo di Sviluppo

1. **Scrittura**: Scrivi il codice in un editor o IDE
2. **Salvataggio**: Salvi il file con estensione appropriata (.py, .js, .java)
3. **Esecuzione**: Il sistema avvia il compilatore o interprete
4. **Debug**: Se ci sono errori, torni al passo 1 per correggerli
5. **Test**: Verifichi che il programma funzioni come previsto

### Errori Comuni

- **Errori di sintassi**: Hai scritto qualcosa in modo scorretto (parole sbagliate, parentesi mancanti)
- **Errori runtime**: Il programma parte ma si blocca durante l'esecuzione (divisione per zero, file non trovato)
- **Errori logici**: Il programma gira ma produce risultati sbagliati

---

## Lezione 1.3: Variabili e Tipi di Dati

### Obiettivi
- Comprendere cosa sono le variabili
- Conoscere i tipi di dati fondamentali
- Sapere come dichiarare e usare variabili

### Le Variabili

Una **variabile** è come un contenitore con un'etichetta. Dentro ci metti un valore che può cambiare (variare) durante l'esecuzione del programma.

```python
# In Python
nome = "Marco"      # Variabile di tipo stringa
eta = 25            # Variabile di tipo intero
altezza = 1.75      # Variabile di tipo decimale
```

In questo esempio:
- `nome`, `eta`, `altezza` sono i **nomi** delle variabili
- `"Marco"`, `25`, `1.75` sono i **valori** contenuti

### Tipi di Dati Fondamentali

#### Numeri Interi (Integer)
Numeri senza parte decimale: 42, -7, 0, 1000000

```python
numero = 42
negativo = -10
zero = 0
```

#### Numeri Decimali (Float)
Numeri con parte decimale: 3.14, -0.5, 2.0

```python
pi = 3.14159
temperatura = 25.5
```

#### Stringhe (String)
Sequenze di caratteri, usate per il testo: "Ciao", 'Python', "123"

```python
saluto = "Ciao mondo!"
nome = 'Marco'
```

#### Booleani (Boolean)
Valori di verità: True (vero) o False (falso)

```python
è_maggiorenne = True
ha_patente = False
```

### Dichiarazione e Assegnazione

In Python non serve dichiarare il tipo di variabile - viene determinato automaticamente:

```python
x = 10          # x è un intero
x = "testo"     # ora x è una stringa
```

In altri linguaggi come Java o C++, devi specificare il tipo:

```java
int x = 10;           // obbligatorio dichiarare il tipo
String nome = "Marco";
```

### Naming (Convenzioni)

Regole per i nomi delle variabili:
- Devono iniziare con una lettera o underscore (_)
- Possono contenere lettere, numeri, underscore
- Non possono contenere spazi
- Sono case-sensitive (maiuscole e minuscole contano)

```python
nome_valido = "ok"
_nome_anch_valido = "ok"
NomeConCammello = "convenzione CamelCase"
nome_minuscolo = "convenzione snake_case"
```

### Operazioni con le Variabili

```python
# Operazioni matematiche
a = 10
b = 3
somma = a + b       # 13
differenza = a - b  # 7
prodotto = a * b    # 30
quoziente = a / b   # 3.333...

# Concatenazione stringhe
nome = "Marco"
cognome = "Rossi"
nome_completo = nome + " " + cognome  # "Marco Rossi"

# Lunghezza stringa
lunghezza = len(nome_completo)  # 10
```

### Esercizi

1. Crea una variabile per il tuo nome, età e città
2. Calcola la somma di due numeri e stampala
3. Unisci due stringhe per formare una frase completa
4. Cambia il valore di una variabile da numero a stringa (in Python)

---

## Riepilogo Modulo 1

### Concetti Chiave
- Il computer esegue istruzioni precise in sequenza
- Il codice sorgente viene tradotto in linguaggio macchina
- Le variabili sono contenitori per valori che cambiano
- Ogni valore ha un tipo (numero, testo, booleano)

### Prossimo Modulo
Nel Modulo 2 affronteremo la logica di programmazione: come prendere decisioni (if/else) e ripetere azioni (cicli).

### Eserzio Finale Modulo 1
Crea un programma che:
1. Definisce variabili per nome, età, hobby preferito
2. Stampa una presentazione usando queste variabili
3. Calcola l'anno di nascita approssimativo