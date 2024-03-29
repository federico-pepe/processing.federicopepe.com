---
title: "Creiamo il nostro primo grafico a barre"
date: "2018-04-22"
categories: 
  - "data"
tags: 
  - "bar-graph"
  - "data"
  - "data-visualization"
  - "grafico-a-barre"
  - "infografiche"
  - "rect"
coverImage: "data-visualization-in-processing.jpg"
---

Abbiamo imparato come [leggere un file CSV](https://blog.federicopepe.com/2018/03/dati-read-file-csv/) in Processing e come cominciare a lavorare sui dati passando [da una tabella a un array](https://blog.federicopepe.com/2018/04/da-una-tabella-csv-agli-array/). Ora è arrivato il momento di creare il nostro primo **grafico a barre**.

Per fare un velocissimo recap: stiamo lavorando in Processing con un file CSV che rappresenta le statistiche metoclimatiche degli ultimi 10 anni (2008-2017) della regione Veneto, prese dal sito del [Mipaaf](https://www.politicheagricole.it/flex/FixedPages/Common/miepfy700_Osservatorio.php/L/IT).

Il file contiene diverse informazioni interessanti ma, per il momento, abbiamo creato un array in cui abbiamo salvato solo i valori delle _temperature minime:_

\[0\] 6.9
\[1\] 7.3
\[2\] 6.7
\[3\] 7.4
\[4\] 7.2
\[5\] 7.7
\[6\] 8.7
\[7\] 8.0
\[8\] 7.6
\[9\] 7.1

Il primo valore si riferisce all'anno 2008 mentre quello inserito alla posizione \[9\] è il dato del 2017.

## Disegniamo il grafico a barre

Disegnare un grafico a barre non è difficile: devo creare dei rettangoli della stessa larghezza e la cui altezza sia legata al dato che voglio rappresentare.

Creiamo una finestra di 500x500 pixel e, siccome i valori sono 10 divido, ciascun rettangolo avrà una larghezza pari a 50 pixel.

Utilizzo un ciclo for per leggere dall'array i singoli valori e li assegno direttamente all'altezza dei rettangoli

```java
/*
 * Creiamo il nostro primo grafico a barre
 * Federico Pepe, 22.04.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

float tempMin[];

void setup() {
  // Dimensione della finestra
  size(500, 500);
  
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());
  
  // Creazione dell'array
  tempMin = new float[0];
  // Inserimento dei dati nell'array
  for(int i = 1; i < csv.getColumnCount(); i++) {
    tempMin = append(tempMin, csv.getFloat(0, i));
  }
  printArray(tempMin);
  // Disegno il grafico
  for(int j = 0; j < tempMin.length; j++) {
    rect(j * 50, 0, 50, tempMin[j]);
  }
  
  noLoop();
}

void draw() {
}
```

La riga di codice più importante è: `rect(j * 50, 0, 50, tempMin[j]);`. Ricordo che la funzione [rect()](https://blog.federicopepe.com/2015/07/primitive-2d-point-line-rect-ellipse-triangle/) accetta quattro parametri: _posizione x, posizione y, larghezza e altezza del rettangolo_. Il codice, quindi, dovrebbe essere chiaro e non dovrebbe necessitare di ulteriori spiegazioni.

[![Grafico a barre in Processing](images/grafico-a-barre-in-processing-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/grafico-a-barre-in-processing.jpg)

Il risultato, come possiamo vedere nell'immagine, non è, però, molto soddisfacente: i grafici a barre generalmente vengono disegnati dal basso verso l'alto e, in questo caso, il valore dell'altezza dei rettangoli è troppo basso per essere comprensibile.

È sufficiente modificare una sola riga di codice:

`rect(j * 50, height, 50, tempMin[j] * - 20);`

per ottenere un risultato completamente differente:

[![Bar Chart in Processing](images/bar-chart-in-processing-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/bar-chart-in-processing.jpg)

Aggiungiamo un po' di margine dai bordi della finestra e tra le varie barre del nostro grafico:

```java
// Disegno il grafico
  int x = 50;
  for(int j = 0; j < tempMin.length; j++) {
    rect(x, height - 50, 36, tempMin[j] * - 20);
    x += 40;
  }
```

e un po' di colore `fill(100, 190, 255);`

[![Visualizzazione di dati in Processing (grafico a barre)](images/data-visualization-in-processing-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/data-visualization-in-processing.jpg)

Ecco il codice completo:

```java
/*
 * Creiamo il nostro primo grafico a barre
 * Federico Pepe, 22.04.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

float tempMin[];

void setup() {
  // Dimensione della finestra
  size(500, 500);
  background(255);
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());
  
  // Creazione dell'array
  tempMin = new float[0];
  // Inserimento dei dati nell'array
  for(int i = 1; i < csv.getColumnCount(); i++) {
    tempMin = append(tempMin, csv.getFloat(0, i));
  }
  printArray(tempMin);
  // Disegno il grafico
  int x = 50;
  fill(100, 190, 255);
  for(int j = 0; j < tempMin.length; j++) {
    rect(x, height - 50, 36, tempMin[j] * - 20);
    x += 40;
  }
  
  noLoop();
}

void draw() {
}
```

Per il momento possiamo fermarci qui. Per chi volesse spingersi un po' oltre, un buon esercizio potrebbe essere, partendo dal codice qui sopra, aggiungere al grafico anche le temperature massime con dei rettangoli colorati di rosso.
