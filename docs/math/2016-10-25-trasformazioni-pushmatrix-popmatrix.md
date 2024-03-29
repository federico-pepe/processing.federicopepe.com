---
title: "Controllare le trasformazioni: pushMatrix() e popMatrix()"
date: "2016-10-25"
categories: 
  - "processing"
tags: 
  - "popmatrix"
  - "pushmatrix"
  - "rotate"
  - "scale"
  - "translate"
  - "trasformazioni"
coverImage: "Trasformazioni_pushMatrix_popMatrix_2.png"
---

Le [funzioni di trasformazione viste nell'ultimo post](https://blog.federicopepe.com/2016/10/trasformazioni-translate-rotate-scale/) ci hanno dato prova di come sia possibile andare a modificare dinamicamente il sistema di [coordinate di Processing](https://blog.federicopepe.com/2015/07/schermo-pixel-e-linee/). In questo articolo, introdurremo due nuove funzioni chiamate _pushMatrix()_ e _popMatrix()_ che, come vedremo insieme, ci permettono di avere maggiore controllo sulle trasformazioni.

## Matrici

Ogni volta che usiamo le funzioni _translate()_, _rotate()_ e _scale()_ andiamo a modificare una **matrice** – in inglese _matrix_. Per spiegarlo nel modo più semplice possibile: una matrice non è altro che un insieme di numeri che descrivono, a livello matematico, come vengono disegnate le geometrie su uno schermo. Le funzioni di trasformazione vanno a modificare questi numeri.

## pushMatrix() e popMatrix()

Le funzioni _pushMatrix()_ e _popMatrix()_ vanno inserite nei nostri programmi sempre in coppia e la loro funzione è quella di salvare lo stato delle trasformazioni (push) e richiamarle (pop) al momento opportuno.

Quando ho cominciato a studiare Processing, non riuscivo a capire il senso di questa cosa. Alla fine, in un video tutorial trovato on-line, ho trovato la similitudine corretta per spiegarlo. Spero che quanto sto per scrivere aiuti anche voi, come è stato per me, a capire meglio il senso di pushMatrix e popMatrix.

Trattandosi di operazioni che facciamo sul sistema delle coordinate, dobbiamo immaginare di spostare il foglio su cui stiamo scrivendo e non la punta della penna con cui scriviamo.

Provo a spiegarmi meglio con un esempio:

```java
void setup() {
  size(500, 500);
}

void draw() {
  background(255);
  translate(100, 0);
  rect(0, 20, 200, 75);
  rect(0, 105, 200, 75);
}
```

In _setup()_ creiamo il nostro canvas di dimensione 500x500 pixel dopodiché in _draw()_ per ogni ciclo della funzione, coloriamo lo sfondo di bianco, spostiamo la punta della nostra penna di 100 pixel verso destra (oppure possiamo pensare che il foglio si sia spostato 100 pixel nella direzione opposta) e poi disegniamo due rettangoli con dimensioni uguali e con valori di x identici e y differente.

Ci aspettiamo, ovviamente, che i due rettangoli siano allineati a sinistra uno con l'altro e infatti questo è risultato:[![pushMatrix e popMatrix in Processing](/assets/images/Trasformazioni_pushMatrix_popMatrix-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/10/Trasformazioni_pushMatrix_popMatrix.png)Se modifichiamo il codice aggiungendo _pushMatrix()_ e _popMatrix()_ ecco che il risultato cambia:

```java
void setup() {
  size(500, 500);
}

void draw() {
  background(255);
  pushMatrix();
  translate(100, 0);
  rect(0, 20, 200, 75);
  popMatrix();
  rect(0, 105, 200, 75);
}
```

[![Come funzionano pushMatrix e popMatrix?](/assets/images/Trasformazioni_pushMatrix_popMatrix_2-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/10/Trasformazioni_pushMatrix_popMatrix_2.png)

Perché il secondo rettangolo non è più allineato con il primo? Quando chiamiamo la funzione pushMatrix() nella nostra matrice viene salvata la posizione corrente del nostro sistema di coordinate, cioè senza alcuna trasformazione perché il comando translate viene invocato successivamente. Dopodiché viene applicato uno spostamento verso destra, viene disegnato il primo rettangolo e, infine, utilizzando popMatrix() ripristiniamo il salvataggio precedente, annullando, cioè, la traslazione di 100 pixel.

In questo modo, il secondo rettangolo, con coordinate 0, 105, verrà disegnato vicino al bordo sinistro della nostra finestra.

## Perché usare pushMatrix() e popMatrix()?

Qualcuno potrebbe chiedersi quale sia l'utilità di utilizzare _pushMatrix()_ e _popMatrix()_ all'interno di uno sketch in Processing. La risposta è abbastanza semplice ma, come scrivevo prima, personalmente non è stata immediata: se realizziamo animazioni complesse con una somma di trasformazioni continue può risultare difficile ricordarsi in ogni momento le coordinate di una determinata forma. Con queste due funzioni possiamo, invece, spostare le coordinate e fare in modo che le nostre figure abbiano sempre coordinate x = 0 e y = 0.
