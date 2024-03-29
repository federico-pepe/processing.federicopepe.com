---
title: "Grafico a barre II"
date: "2018-04-29"
categories: 
  - "data"
tags: 
  - "data-visualization"
  - "grafico-a-barre"
  - "processing"
  - "visualizzazione-di-dati"
coverImage: "Grafico-a-barre-con-riferimenti-4.jpg"
---

Nell'articolo precedente abbiamo cominciato a lavorare al nostro [primo grafico a barre](https://blog.federicopepe.com/2018/04/grafico-a-barre-in-processing/) utilizzando come fonte i dati presenti all'interno di un file CSV.

In questo articolo andremo a completare la visualizzazione inserendo anche le temperature massime e dei riferimenti.

## Array delle temperature massime

I dati relativi alle temperature massime sono già presenti dentro al file CSV. Come [abbiamo già visto](https://blog.federicopepe.com/2018/04/da-una-tabella-csv-agli-array/), per comodità inseriamo questi dati in un array.

Dove abbiamo dichiarato le variabili, aggiungiamo:

```java
float tempMin[], tempMax[];
```

Inizializziamo l'array:

```java
tempMax = new float[0];
```

Inseriamo i dati utilizzando lo stesso ciclo for per non appesantire troppo il programma

```java
for (int i = 1; i < csv.getColumnCount(); i++) {
  tempMin = append(tempMin, csv.getFloat(0, i));
  tempMax = append(tempMax, csv.getFloat(3, i));
}
```

## Grafico a barre delle temperature massime

Utilizzando sempre il codice che abbiamo già scritto, aggiungiamo nel ciclo for in cui andavamo a disegnare i rettangoli delle temperature minime, quelli relativi alle massime. Per differenziarle a livello visivo utilizzeremo il colore rosso.

```java
fill(255, 100, 100);
rect(x, height - 50, 36, tempMax[i] * - 20);
```

Siccome i rettangoli rossi saranno più alti rispetto a quelli azzurri, assicuriamoci di disegnarli per primi.

Nel mio codice ho aggiunto anche un `noStroke()` per eliminare il bordo.

[![Grafico a barre con temperature massime](images/Grafico-a-barre-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/Grafico-a-barre.jpg)

## Aggiungiamo dei riferimenti

Quando si creano delle visualizzazioni di dati può essere utile dare dei riferimenti a chi sta osservando il nostro lavoro per aiutarli nella comprensione. L'immagine qui sopra presa singolarmente potrebbe rappresentare migliaia di cose differenti.

Aggiungere delle linee di riferimento è questione di un semplice ciclo for:

```java
for (int j = 0; j <= 20; j++) {
  stroke(0, 30);
  line(30, height - 50 + (j * - 20), 470, height - 50 + (j * - 20));
}
```

[![Grafico a barre con riferimenti in Processing](images/Grafico-a-barre-con-riferimenti-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/Grafico-a-barre-con-riferimenti.jpg)

Ora non ci resta che aggiungere il testo (aggiungiamo un paio di linee di codice al precedente ciclo for):

```java
textAlign(RIGHT, CENTER);
for (int j = 0; j <= 20; j++) {
  fill(0, 127);
  text(j + "°", 25, height - 52 + (j * - 20));
  stroke(0, 30);
  line(30, height - 50 + (j * - 20), 470, height - 50 + (j * - 20));
}
```

[![Grafico a barre in Processing](images/Grafico-a-barre-con-riferimenti-2-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/Grafico-a-barre-con-riferimenti-2.jpg)

Per rendere il grafico più leggibile facciamo dei piccoli miglioramenti: scriviamo il valore numerico ogni cinque gradi e schiariamo leggermente le altre linee:

```java
textAlign(RIGHT, CENTER);

for (int j = 0; j <= 20; j++) {
  if (j % 5 == 0) {
    fill(0, 127);
    text(j + "°", 25, height - 52 + (j * - 20));
    stroke(0, 30);
  } else {
    stroke(0, 15);
  }
  line(30, height - 50 + (j * - 20), 470, height - 50 + (j * - 20));
}
```

[![Realizzare un grafico a barre in Processing](images/Grafico-a-barre-con-riferimenti-3-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/Grafico-a-barre-con-riferimenti-3.jpg)

Non ci resta che aggiungere l'anno di riferimento in fondo al grafico: avendo aggiunto l'opzione _header_ nella lettura del file CSV viene saltata completamente la prima riga che include proprio questo dato. Potremmo riscrivere il codice ma, per questa volta, adotteremo una soluzione più semplice anche se non proprio elegante. Per completezza includo tutto il codice del programma:

```java
/*
 * Grafico a barre, 2
 * Federico Pepe, 29.04.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

float tempMin[], tempMax[];

void setup() {
  size(500, 500);
  background(255);
  noStroke();
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());

  tempMin = new float[0];
  tempMax = new float[0];

  for (int i = 1; i < csv.getColumnCount(); i++) {
    tempMin = append(tempMin, csv.getFloat(0, i));
    tempMax = append(tempMax, csv.getFloat(3, i));
  }

  printArray(tempMin);

  println("Il valore minimo è: " + min(tempMin));
  println("Il valore massimo è: " + max(tempMin));

  noLoop();

  int x = 50;
  int year = 2008;

  for (int i = 0; i < tempMin.length; i++) {
    fill(255, 100, 100);
    rect(x, height - 50, 36, tempMax[i] * - 20);
    fill(100, 190, 255);
    rect(x, height - 50, 36, tempMin[i] * - 20);
    fill(0, 127);
    text(year, x + 2, height - 30);
    x += 40;
    year++;
  }

  textAlign(RIGHT, CENTER);

  for (int j = 0; j <= 20; j++) {
    if (j % 5 == 0) {
      fill(0, 127);
      text(j + "°", 25, height - 52 + (j * - 20));
      stroke(0, 30);
    } else {
      stroke(0, 15);
    }
    line(30, height - 50 + (j * - 20), 470, height - 50 + (j * - 20));
  }
}

void draw() {
}
```

[![Bar Graph in Processing](images/Grafico-a-barre-con-riferimenti-4-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/04/Grafico-a-barre-con-riferimenti-4.jpg)
