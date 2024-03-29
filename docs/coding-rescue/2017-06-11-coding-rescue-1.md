---
title: "Coding Rescue #1 - Invertire sotto-sopra una porzione di un'immagine"
date: "2017-06-11"
categories: 
  - "coding-rescue"
tags: 
  - "coding-rescue"
  - "image"
  - "intlist"
  - "loadpixel"
coverImage: "Coding-Rescue-1-Processing-invertire-sottosopra-porzione-immagine.jpg"
---

# Coding Rescue #1 - Invertire sotto-sopra una porzione di un'immagine

Inauguro oggi con questo post una rubrica chiamata **Coding Rescue** ovvero: come risolvere problemi di programmazione che mi vengono posti dai lettori del blog. Ogni tanto capita che qualcuno mi scriva privatamente perché è rimasto bloccato con un esercizio in Processing che non riesce a risolvere e mi viene chiesto di dare una mano a trovare una soluzione.

Mi piace ricevere questo genere di messaggi perché mi permette di scontrarmi con difficoltà a cui non avevo mai pensato. Dal momento che capita a tutti – sottoscritto compreso – di rimanere bloccati per giorni, penso che aiutare le persone sia un ottimo modo per allenarsi e imparare qualcosa di nuovo.

## Il problema

Qualche giorno fa ho ricevuto il seguente messaggio sulla [mia pagina Facebook](https://www.facebook.com/fedpep/):

> creare un progettino, ovvero una funzione, che inverte (sotto sopra) l'immagine, solo all'interno di un quadrato che si crea intorno al puntatore del mouse.

Il problema è interessante perché pone una serie di sfide che, sommate, non sono per nulla semplici:

1. Dobbiamo lavorare con un'immagine
2. Lo script deve essere dinamico perché in relazione alla posizione del puntatore del mouse
3. Dobbiamo invertire sotto sopra una porzione di un'immagine

Come consiglio sempre: è importante concentrarsi sui vari punti uno per volta perché, altrimenti, si rischia di non arrivare facilmente alla soluzione.

## La soluzione in pseudo-codice

Prima di cominciare a scrivere il codice, proviamo a descrivere il funzionamento del programma a parole; ho sottolineato con il corsivo le parole chiave: il nostro sketch dovrà, all'_avvio_, caricare un'_immagine_. Intorno alla posizione del mouse _disegneremo_ un quadrato e, una volta _analizzati i pixel_ presenti all'interno di questo quadrato, _creeremo_ e _disegneremo_ una nuova immagine che avrà _dimensione pari a quella del quadrato_ i cui pixel, rispetto all'originale, _saranno invertiti sotto-sopra_.

## La soluzione: passo dopo passo

### 1\. Carichiamo l'immagine

Per prima cosa dobbiamo ripassare come si lavora sulle immagini:

- [Utilizzare immagini in Processing: PImage, loadimage() e image()](https://blog.federicopepe.com/2017/03/utilizzare-immagini-in-processing/)
- [Array di pixel: loadPixels() e updatePixels()](https://blog.federicopepe.com/2017/03/array-pixel-loadpixels-updatepixels/)

Per risolvere il problema avremo bisogno di due oggetti immagine: il primo sarà l'immagine originale mentre, la seconda, sarà l'immagine con i pixel invertiti che chiamerò _flipped_. Avremo inoltre bisogno di impostare una variabile che determinerà la larghezza del quadrato e, di conseguenza, la grandezza dell'immagine che andrò a creare. Per questo esercizio, ho deciso di usare [la foto di un corgi](http://buzzsharer.com/wp-content/uploads/2016/10/corgi-photo.jpg).

Nella funzione draw, per il momento, mi preoccupo solo di disegnare un quadrato intorno alla posizione del mouse.

```java
/*
 * Coding Rescue #1 - Invertire sotto-sopra una porzione di un'immagine
 * Federico Pepe, 11.06.2017
 * http://blog.federicopepe.com/processing
 */

// Creo i due oggetti immagine
PImage img, flipped;

// Variabile che determina la larghezza del quadrato
int w = 100;

void setup() {
  size(700, 542);
  // Carico l'immagine originale e la disegno
  img = loadImage("corgi-photo.jpg");
  image(img, 0, 0);
  // Creo l'immagine flipped
  flipped = createImage(w, w, RGB);
  noFill();
}

void draw() {
  image(img, 0, 0);

  rectMode(CENTER);
  rect(mouseX, mouseY, w, w);
}
```

### 2\. Carichiamo i pixel di riferimento in un array

Il prossimo passaggio sarà analizzare i pixel all'interno del quadrato disegnato e inserirli uno per uno all'interno di un array: avendo come riferimento la posizione del mouse e volendo tenere quel punto al centro del quadrato creo quattro variabili: _startX, startY, endX_ ed _endY_ che mi serviranno come riferimento per i cicli for.

Invece di utilizzare un array classico, decido di usare una variabile di tipo [**IntList**](https://processing.org/reference/IntList.html) questo perché si tratta di un tipo di dato più flessibile che gestisce gli elementi al suo interno in modo più dinamico e rapido. Operazioni quali l'aggiunta, la modifica, la lettura dei dati al suo interno sono più veloci e semplici da eseguire rispetto ai comuni array.

```java
/*
 * Coding Rescue #1 - Invertire sotto-sopra una porzione di un'immagine
 * Federico Pepe, 11.06.2017
 * http://blog.federicopepe.com/processing
 */

// Creo i due oggetti immagine
PImage img, flipped;

// Variabile che determina la larghezza del quadrato
int w = 100;

// Variabile nella quale inserirò tutti i pixel analizzati
IntList arrayPixel = new IntList();

void setup() {
  size(700, 542);
  // Carico l'immagine originale e la disegno
  img = loadImage("corgi-photo.jpg");
  image(img, 0, 0);
  // Creo l'immagine flipped
  flipped = createImage(w, w, RGB);
  noFill();
}

void draw() {
  image(img, 0, 0);
  
  int startX = mouseX-w/2;
  int startY = mouseY-w/2;
  int endX = mouseX + w/2;
  int endY = mouseY + w/2;
  
  img.loadPixels();
  
  for (int y = startY; y < endY; y++) {
    for (int x = startX; x < endX; x++) {
      arrayPixel.append(get(x, y));
    }
  }
  
  rectMode(CENTER);
  rect(mouseX, mouseY, w, w);
}
```

**Problema:**

In questo momento ad ogni iterazione di draw, la variabile **arrayPixel**, grazie alla funzione **append()**, viene ingrandita di 10.000 valori (100\*100). Per vedere cosa accade, provate ad aggiungere: `println(arrayPixel.size());`. Se provassimo a disegnare un'immagine con una dimensione variabile, il programma andrebbe in crash. È importante, dunque, svuotare l'array prima dei cicli for con la funzione **clear()**: `arrayPixel.clear();`

### 3\. Aggiungiamo i pixel analizzati nell'immagine di destinazione

Ora che i pixel contenuti nel quadrato di riferimento sono stati aggiunti all'array dobbiamo trasferirli tutti all'interno della nostra immagine di destinazione che abbiamo creato in precedenza.

Carichiamo, quindi, i pixel dell'immagine di destinazione e, attraverso un ciclo for, assegniamo a ogni pixel il pixel relativo presente all'interno dell'array:

```java
flipped.loadPixels();
for (int i = 0; i < arrayPixel.size(); i++) {
  flipped.pixels[i] = arrayPixel.get(i);
}
flipped.updatePixels();
```

Aggiungendo `image(flipped, 0, 0);` alla fine del ciclo draw e cliccando su Run dovreste vedere in alto a sinistra un quadrato di 100 pixel contenente la stessa immagine del quadrato di riferimento disegnato intorno alla posizione del mouse.

Ora non ci resta che completare il lavoro.

### 4\. Invertire l'immagine di destinazione sotto-sopra

Mentre lavoravo all'esercizio, arrivato a questo punto mi sono bloccato. Per invertire un'immagine sottosopra avrei dovuto modificare l'ultimo ciclo for scritto per fare in modo che i pixel venissero scritti nell'immagine di destinazione invertiti rispetto all'originale. Su questa cosa ho sbattuto la testa per qualche giorno poi è arrivata l'illuminazione: anziché andare a complicarmi la vita con i pixel, avrei potuto usare le [funzioni di trasformazione](https://blog.federicopepe.com/2016/10/trasformazioni-translate-rotate-scale/).

In particolare, dopo aver fatto una veloce ricerca, se passiamo valori negativi alla funzione **scale()**, otteniamo l'immagine invertita.

```java
pushMatrix();
translate(startX, startY+w);
scale(1, -1);
image(flipped, 0, 0);
popMatrix();
```

Ecco che con queste poche righe di codice, siamo giunti alla fine: se non vi ricordate come funzionano, potete [ripassare pushMatrix() e popMatrix() a questo indirizzo](https://blog.federicopepe.com/2016/10/trasformazioni-pushmatrix-popmatrix/).

### Risultato finale:

![](/assets/images/giphy.gif)
