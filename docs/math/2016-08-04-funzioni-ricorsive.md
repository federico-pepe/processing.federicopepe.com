---
title: "Funzioni ricorsive"
date: "2016-08-04"
categories: 
  - "processing-math"
tags: 
  - "funzioni-ricorsive"
  - "recursion"
  - "ricorsivita"
coverImage: "Processing_Funzioni_Ricorsive.png"
---

In programmazione definiamo **ricorsive** quelle funzioni che richiamo se stesse all'interno di un programma. A parole si tratta di un concetto molto semplice ma è bene fare qualche esempio per fugare ogni possibile dubbio.

Prima di procedere è bene puntualizzare che quando creiamo e usiamo queste funzioni dobbiamo fare attenzione a inserire sempre una condizione di uscita altrimenti lo sketch andrà in _StackOverflowError._

## Funzioni ricorsive: removeOne();

Ecco il primo esempio:

```java
/*
 * Funzioni Ricorsive
 * by Federico Pepe
 *
*/

void setup() {
  noLoop();
}

void draw() {
  removeOne(5);
}

void removeOne(int n) {
  println(n);
  if(n > 1) {
    n--;
    removeOne(n);
  }
}
```

Analizziamo il funzionamento: tramite il comando _noLoop()_ in _setup()_ sappiamo che la funzione _draw()_ verrà ripetuta una sola volta. Dopodiché creiamo la nostra funzione **removeOne()** che, ogni volta che viene chiamata, eseguirà i seguenti comandi:

- stampa in console il valore di _n_
- controlla se il valore di _n_ è maggiore di 1 se _true_
    - sottrai 1 a _n_
    - richiama la funzione _removeOne_ passando il nuovo valore di _n_

Il risultato in console sarà, ovviamente:

5
4
3
2
1

**Nota:** spostando n--; dopo removeOne(n), il programma andrà in un loop infinito generando un errore: _StackOverflowError._ Gli sviluppatori di Processing sono stati così furbi da riconoscere questo tipo di errore e da far stoppare automaticamente il programma evitando, così, di far bloccare il computer.

Fino a qui niente di eccezionale, avremmo potuto ottenere lo stesso risultato in mille modi diversi utilizzando, ad esempio, un ciclo for. Le cose possono diventare interessanti quando cominciamo a utilizzare le funzioni ricorsive per disegnare qualcosa sullo schermo come nel secondo esempio:

## Funzioni ricorsive: drawCircle();

![Funzioni Ricorsive](/assets/images/Processing_Funzioni_Ricorsive-1024x673.png)

```java
/*
 * Funzioni Ricorsive: drawCircle()
 * by Federico Pepe
 *
*/

void setup() {
  size(700, 400);
  noLoop();
  noFill();
  background(255);
}

void draw() {
  drawCircle(width/2, height/2, width/2, 7);
}

void drawCircle(int x, int y, int radius, int recursion) {
  ellipse(x, y, radius, radius);
  if (recursion > 1) {
    recursion--;
    drawCircle(x + radius/2, y, radius/2, recursion);
    drawCircle(x - radius/2, y, radius/2, recursion);
  }
}
```

Il classico esempio che si vede quando si parla di ricorsività: utilizziamo una variabile per definire quante ripetizioni dovranno esserci (in questo caso 7) e poi disegniamo dei cerchi la cui posizione _x_ e il cui raggio vengono dimezzati ogni volta. Per vedere i singoli passaggi potete modificare manualmente l'ultimo parametro in drawCircle() oppure creare una nuova variabile che [viene incrementata alla pressione del mouse](https://gist.github.com/federico-pepe/a835bc8e4bdeeb95afe4c47144e40943).
