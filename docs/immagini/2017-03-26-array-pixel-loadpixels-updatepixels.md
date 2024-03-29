---
title: "Array di pixel: loadPixels() e updatePixels()"
date: "2017-03-26"
categories: 
  - "processing-images"
tags: 
  - "2d-array"
  - "loadpixels"
  - "pixels-length"
  - "updatepixels"
---

Avevo parlato di pixel in uno dei [primissimi post](https://blog.federicopepe.com/2015/07/schermo-pixel-e-linee/) su Processing in questo blog. Grazie alle competenze che abbiamo acquisito nelle ultime settimane, possiamo fare un ulteriore passo in avanti.

Le funzioni che abbiamo usato fino a oggi ci hanno permesso di disegnare linee e forme sullo schermo o, come visto di recente, di [mostrare un'immagine](https://blog.federicopepe.com/2017/03/utilizzare-immagini-in-processing/). Queste funzioni che, all'apparenza, sembrano eseguire operazioni molto semplici, in realtà nascondono un principio molto complesso: stabilire se ciascun pixel sullo schermo deve essere accesso o spento e, se acceso, il [colore](https://blog.federicopepe.com/2015/08/colori-rgb/) che deve rappresentare.

## Array di pixel

Siamo abituati a pensare ai pixel come ad una griglia sullo schermo; quindi ad un [array bidimensionale](https://blog.federicopepe.com/2016/07/2d-perlin-noise/).

![](/assets/images/Processing-Pixel-Array-1d.jpg)

In Processing, però, il valore di ciascuno di essi viene salvato in un classico array monodimensionale.

![](/assets/images/Processing-Pixel-Array-monodimensionale-2.jpg)

È possibile accedere a queste informazioni e modificarle a nostro piacimento? Ovviamente si, utilizzando le funzioni **loadPixels()** e **updatePixels()**.

## loadPixels() e updatePixels()

Con la prima funzione stiamo dicendo a Processing che intendiamo lavorare sull'array di pixel e che, quindi, deve caricarlo in una variabile. _updatePixels()_, invece, la usiamo quando abbiamo apportato tutte le modifiche e vogliamo che il programma aggiorni le informazioni sullo schermo.

Facciamo un esempio pratico:

```java
/*
 * Array di pixel: loadPixels() e updatePixels()
 * Federico Pepe, 26.03.2017
 * http://blog.federicopepe.com/processing
 */

void setup() {
  size(500, 500);
  loadPixels();  
 
  for (int i = 0; i < pixels.length; i++) {
    float rand = random(255);
    color c = color(0, 0, rand);
    pixels[i] = c;
  }
  
  updatePixels();
}
```

In questo programma carichiamo tutti i valori di una finestra di 500x500 pixel. Con il ciclo _for_ partiamo dal primo valore presente nel nostro array e arriviamo fino all'ultimo, identificato, per comodità, dalla [funzione](https://blog.federicopepe.com/2016/01/array/) `pixel.length` e assegniamo a ciascuno un colore casuale `float rand = random(255);` nella scala dei blu `color c = color(0, 0, rand);`.

Assegniamo il nuovo colore al pixel `pixels[i] = c;` e, una volta usciti dal loop, chiediamo a Processing di aggiornare e mostrare tutte le modifiche che abbiamo effettuato `updatePixels();`.

Il risultato sarà il seguente:

![Pixel Array Blu](/assets/images/Processing-Pixel-Array-Blu-988x1024.png)

## Modificare un pixel conoscendone la posizione x e y

A questo punto, immagino, potrà esservi sorta spontaneamente una domanda: è possibile accedere a un determinato pixel conoscendone la posizione x e y all'interno della finestra come siamo stati abituati a fare fino a ora?

Riprendendo l'immagine della griglia più sopra, proviamo a capire come accedere al pixel 19: la sua posizione è x = 5, y = 2. A questo punto è importante ricordare che, per questi valori, partiamo a contare da 0 mentre, per la larghezza della finestra, da 1.

Ora dobbiamo sommare il valore di x al valore di y moltiplicato alla larghezza.

La formula è, dunque: `x + (y * width)`

5 + (2 \* 7) = 19

I conti tornano!

Proviamo a modificare il codice di prima come segue:

```java
/*
 * Array di pixel: loadPixels() e updatePixels()
 * Federico Pepe, 26.03.2017
 * http://blog.federicopepe.com/processing
 */

void setup() {
  size(500, 500);
  loadPixels();  
  color c;
  for (int x = 0; x < width; x++) {
    for (int y = 0; y < height; y++) {
      float rand = random(255);
      int pos = x + y * width;
      if(x % 2 == 0) {
        c = color(0, 0, rand);
      } else {
        c = color(rand, 0, 0);
      }
      pixels[pos] = c;
    }
  }
  
  updatePixels();
}
```

![](/assets/images/Processing-loadPixels-updatePixels-example-2-988x1024.png)

Zoomando l'immagine noterete che una riga è rossa e una riga è, invece, blu. Il prossimo passo sarà applicare quello che abbiamo appena imparato su un'immagine. Provate a pensare a tutte le operazioni che potremmo compiere andando a modificare individualmente ogni singolo pixel.
