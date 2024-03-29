---
title: "Grafico a linee"
date: "2018-05-20"
categories: 
  - "data"
tags: 
  - "beginshape"
  - "data-visualization"
  - "endshape"
  - "grafico-a-linee"
  - "infografiche"
  - "vertex"
coverImage: "Grafico-a-linee-in-Processing-finale.jpg"
---

Partiamo sempre dall'esempio su cui stiamo lavorando da un po' di tempo a questa parte e creiamo un **grafico a linee** in Processing.

L'unica modifica al codice che dobbiamo fare è quella relativa alla grafica: lasciamo, dunque, inalterata la prima parte, quella relativa alla [lettura dei dati dal file .csv](https://blog.federicopepe.com/2018/03/dati-read-file-csv/) e l'inserimento degli [stessi in un array](https://blog.federicopepe.com/2018/04/da-una-tabella-csv-agli-array/) e passiamo direttamente alla grafica.

## Ripensare la posizione della x

La prima differenza rispetto al [grafico a barre](https://blog.federicopepe.com/2018/04/grafico-a-barre-in-processing/) sarà determinare correttamente la posizione x del valore estratto dall'array. Se, infatti, il ciascuna barra del grafico aveva una sua larghezza, ora dobbiamo rappresentare solo un punto.

Per risolvere il problema, pur mantenendo il [risultato finale che avevamo realizzato nell'ultimo post](https://blog.federicopepe.com/2018/04/grafico-a-barre-2/), creo una nuova variabile chiamata _x1_ che mi servirà come nuovo riferimento e aggiungo un nuovo ciclo for solo per disegnare i punti di riferimento nel grafico.

```java

int x1 = 68;
  
for(int i = 0; i < tempMin.length; i++) {
  ellipse(x1, height - 50 + tempMin[i] * - 20, 10, 10);
  ellipse(x1, height - 50 + tempMax[i] * - 20, 10, 10);
  x1 += 40;
}
```

Ecco il risultato:

[![Grafico a linee in Processing](images/Grafico-a-linee-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/05/Grafico-a-linee.jpg)

## Creiamo il grafico a linee

Creare un grafico a linee potrebbe essere più complesso di quanto ipotizzato: dovremmo, infatti, creare manualmente una linea per congiungere tra loro i punti disegnati in precedenza.

Per fortuna ci vengono in aiuto alcune funzione di Processing: [**beginShape()**](https://processing.org/reference/beginShape_.html), [**vertex()**](https://processing.org/reference/vertex_.html) ed [**endShape()**](https://processing.org/reference/endShape_.html).

Con _beginShape()_ diciamo al programma di iniziare a creare una forma, aggiungiamo tutti i vertici che la compongono con _vertex()_ e, una volta richiamata la funzione _endShape()_, Processing si preoccuperà di collegare insieme tutti i punti.

Come al solito, consiglio di verificare sul _reference_ i parametri opzionali che possiamo usare per ciascuna funzione. Per questo esempio il comportamento di default è quello che fa al caso nostro ma in futuro potrebbero tornarvi utili anche le altre possibilità.

Dovendo creare due grafici a barre, dovremo utilizzare due cicli for:

```java

int x1 = 68;

beginShape();
for (int i = 0; i < tempMin.length; i++) {
  vertex(x1, height - 50 + tempMin[i] * - 20);
  ellipse(x1, height - 50 + tempMin[i] * - 20, 10, 10);
  x1 += 40;
}
endShape();

x1 = 68;
beginShape();
for (int i = 0; i < tempMax.length; i++) {
  vertex(x1, height - 50 + tempMax[i] * - 20);
  ellipse(x1, height - 50 + tempMax[i] * - 20, 10, 10);
  x1 += 40;
}
endShape();
```

[![Grafico a linee beginShape, vertex, endShape](images/Grafico-a-linee-in-Processing-vertex-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/05/Grafico-a-linee-in-Processing-vertex.jpg)

A questo punto possiamo eliminare i grafici a barre che avevamo tenuto come riferimento e andare a sistemare i colori per ottenere un risultato finale soddisfacente:

[![Grafico a linee finale in Processing](images/Grafico-a-linee-in-Processing-finale-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/05/Grafico-a-linee-in-Processing-finale.jpg)

## Codice completo

Guardando il codice vi sembrerà un po' verboso, in particolare per quanto riguarda le assegnazioni dei colori. Facendo qualche esperimento vi renderete conto di quanto sia importante inserire le istruzioni giuste per evitare problemi di visualizzazione.

```java

/*
 * Grafico a linee
 * Federico Pepe, 20.05.2018
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

  // Scritte relative all'anno
  int x = 50;
  int year = 2008;
  
  for (int i = 0; i < tempMin.length; i++) {
    fill(0, 127);
    text(year, x + 2, height - 30);
    x += 40;
    year++;
  }
  
  // Temperature minime
  int x1 = 68;
  beginShape();
  for (int i = 0; i < tempMin.length; i++) {
    fill(100, 190, 255);
    vertex(x1, height - 50 + tempMin[i] * - 20);
    noStroke();
    ellipse(x1, height - 50 + tempMin[i] * - 20, 10, 10);
    x1 += 40;
    stroke(100, 190, 255);
    noFill();
  }
  endShape();
  
  // Temperature massime
  x1 = 68;
  beginShape();
  for (int i = 0; i < tempMax.length; i++) {
    fill(255, 100, 100);
    vertex(x1, height - 50 + tempMax[i] * - 20);
    noStroke();
    ellipse(x1, height - 50 + tempMax[i] * - 20, 10, 10);
    x1 += 40;
    stroke(255, 100, 100);
    noFill();
  }
  endShape();

  // Griglia di riferimento
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
