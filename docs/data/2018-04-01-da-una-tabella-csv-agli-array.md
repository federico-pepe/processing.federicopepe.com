---
title: "Da una tabella CSV agli array"
date: "2018-04-01"
categories: 
  - "data"
tags: 
  - "append"
  - "array"
  - "csv"
  - "dati"
  - "getfloat"
  - "getint"
  - "getstring"
  - "table"
coverImage: "Da-una-tabella-CSV-agli-array-1.jpg"
---

Una volta capito come [leggere](https://blog.federicopepe.com/2018/03/dati-read-file-csv/) con Processing i dati contenuti in un file CSV, il passaggio successivo è rendere questi dati leggibili e modificabili facilmente all'interno del programma convertendoli in variabili e array.

Ripartiamo dal nostro esempio precedente utilizzando sempre lo stesso [data set](https://goo.gl/rp8STm):

```java
/*
 * Leggere file CSV
 * Federico Pepe, 25.03.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

void setup() {
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());
  
  for(int i = 0; i < csv.getRowCount(); i++) {
    println(csv.getFloat(i, 2));
  }
  
  noLoop();
}

void draw() {
}
```

Prima di procedere, assicuriamoci che il programma funzioni cliccando su _run_: nella console dovrebbero comparire i dati contenuti nella colonna relativa al 2009.

## Utilizzare i metodi corretti per leggere i dati

Un aspetto importante da tenere presente è di utilizzare i metodi corretti per accedere ai dati. Spulciando nel [reference di Table](https://processing.org/reference/Table.html) noterete che esistono diverse funzioni come [**.getFloat()**](https://processing.org/reference/Table_getFloat_.html), [**.getInt()**](https://processing.org/reference/Table_getInt_.html), [**.getString()**](https://processing.org/reference/Table_getString_.html).

Se sostituiamo nell'esempio precedente la riga `println(csv.getFloat(i, 2));` con `println(csv.getString(i, 2));` Processing non genererà nessun errore e continuerà a far girare il nostro programma ma, ora, quei valori sono considerati stringhe (quindi testo) e non più numeri.

Tutti questi metodi accettano due parametri: il primo indica la riga della tabella, il secondo la colonna. Per quest'ultimo possiamo usare sia un numero, partendo, come sempre a contare da 0, oppure una stringa contenente il nome della colonna.

Il codice, può essere sostituito con: `println(csv.getFloat(i, "2009"));`

Se sostituite sempre la stessa riga con `println(csv.getFloat(i, "Descrizione"));` la console vi restituirà tutti valori _NaN_ ovvero _Not a Number_. Come dicevo, il programma continuerà a funzionare ma non in modo corretto.

## Dal tabella CSV all'array

Passare tutti i dati in un array può essere molto comodo per utilizzare alcune funzioni specifiche di calcolo, come, ad esempio, **min()** e **max()** che restituiscono, rispettivamente, il valore minimo e massimo di un array.

Anche se in questo momento siamo ancora lontani dall'idea di creare una visualizzazione di dati, dovremmo comunque cominciare a pensare a come utilizzeremo questi numeri.

Per come è stato strutturato il file CSV, ciascuna colonna rappresenta un anno con valori di vario tipo: temperatura minima, temperatura massima, eccetera; ma se noi volessimo rappresentare la variazione di uno stesso valore nel tempo dovremmo lavorare orizzontalmente e non verticalmente.

Sfruttiamo questo esempio per capire come passare i dati dal CSV a un array:

Creiamo un array di tipo float chiamato _tempMin_ nel quale inseriremo tutti i valori di temperatura minima e modifichiamo il nostro ciclo _for_ per girare non più sul numero di righe ma su quello delle colonne. Impostiamo l'inizio del ciclo for a 1 per saltare la prima colonna.

```java
/*
 * Da una tabella CSV agli array
 * Federico Pepe, 01.04.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

float tempMin[];

void setup() {
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());
  
  tempMin = new float[csv.getColumnCount()];
    
  for(int i = 1; i < csv.getColumnCount(); i++) {
    tempMin[i] = csv.getFloat(0, i);
  }
  
  printArray(tempMin);
  
  noLoop();
}

void draw() {
}
```

La dimensione dell'array è uguale al numero di colonne all'interno del file `tempMin = new float[csv.getColumnCount()];` e inseriamo all'interno dell'array i valori float provenienti dalla riga 0, perché stiamo ignorando l'header, e di ciascuna colonna: `tempMin[i] = csv.getFloat(0, i);`

Dal risultato in console notiamo subito un problema: il primo valore dell'array è _0.0_ perché, effettivamente, l'array contiene un valore in più, quello della colonna _Descrizione_.

Abbiamo due possibilità per risolvere il problema:

Modificare la grandezza dell'array sottraendo 1: `tempMin = new float[csv.getColumnCount()-1];` e modificando l'inserimento dei valori nell'array sempre spostando l'indice indietro di 1 `tempMin[i-1] = csv.getFloat(0, i);`.

Questa soluzione funziona ma non è molto elegante, meglio cambiare il codice come segue: inizializziamo l'array con grandezza pari a 0: `tempMin = new float[0];` e poi utilizziamo la funzione **append()** che espande l'array di un elemento e aggiunge il dato nella nuova posizione `tempMin = append(tempMin, csv.getFloat(0, i));`

## Il codice completo

```java
/*
 * Da una tabella CSV agli array
 * Federico Pepe, 01.04.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

float tempMin[];

void setup() {
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());
  
  tempMin = new float[0];
    
  for(int i = 1; i < csv.getColumnCount(); i++) {
    tempMin = append(tempMin, csv.getFloat(0, i));
  }
  
  printArray(tempMin);
  
  noLoop();
}

void draw() {
}
```

Ora l'array è corretto e contiene esattamente tutti i valori previsti. Come dicevo, ora possiamo sfruttare l'array per ottenere il valore minimo e quello massimo molto semplicemente:

```java
println("Il valore minimo è: " + min(tempMin));
println("Il valore massimo è: " + max(tempMin));
```
