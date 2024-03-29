---
title: "Processare le immagini in Processing"
date: "2017-04-29"
categories: 
  - "processing-images"
tags: 
  - "blue"
  - "color"
  - "constrain"
  - "green"
  - "map"
  - "red"
coverImage: "Processare-immagini-Processing.png"
---

In questo post vedremo come unire le nozioni che abbiamo appreso relativamente [al caricamento e all' utilizzo delle immagini in Processing](https://blog.federicopepe.com/2017/03/utilizzare-immagini-in-processing/) e alle possibilità creative che abbiamo a disposizione [lavorando sui singoli pixel](https://blog.federicopepe.com/2017/03/array-pixel-loadpixels-updatepixels/) per imparare a processore le immagini a nostro piacimento.

Riprendiamo l'[immagine del gatto](https://i0.wp.com/blog.federicopepe.com/wp-content/uploads/2017/03/cat-300572_640.jpg?w=640&ssl=1) che abbiamo già [usato in precedenza](https://blog.federicopepe.com/2017/03/modificare-immagini-tint-filtro/) e carichiamola all'interno di un nuovo sketch. Invece di utilizzare la funzione _image()_ per mostrarla nella finestra, questa volta andremo a caricare tutti i pixel che compongono l'immagine.

```java
/*
 * Processare le immagini in Processing
 * Federico Pepe, 29.04.2017
 * http://blog.federicopepe.com/processing
 */

PImage img;

void setup() {
  size(640, 536);
  img = loadImage("cat-300572_640.jpg");
}

void draw() {
  // Carichiamo i pixel della finestra
  loadPixels();
  // Carichiamo i pixel dell'immagine
  img.loadPixels();
  for(int y = 0; y < height; y++) {
    for(int x = 0; x < width; x++) {
      int pos = x + y * width;
      
      float r = red(img.pixels[pos]);
      float g = green(img.pixels[pos]);
      float b = blue(img.pixels[pos]);
      
      pixels[pos] = color(r, g, b);
    }
  }
  updatePixels();
}
```

Analizziamo velocemente il codice qui sopra concentrandoci, in particolare, sulle cose che non abbiamo mai visto prima: come indicato nei commenti, oltre a caricare i pixel della finestra dobbiamo caricare anche quelli relativi all'immagine. Per farlo utilizziamo `img.loadPixels();` dove _img_ fa riferimento al nome della variabile che abbiamo dichiarato all'inizio del programma.

Con due loop for andiamo a caricare ogni singolo pixel e, utilizzando le funzioni **red()**, **green()**, **blue()** otteniamo i valori R, G e B. Attraverso `pixels[pos] = color(r, g, b);` assegniamo i valori al pixel sullo schermo.

Il nostro programma, in pratica, lavora come segue: che valori di _rosso_, _verde_ e _blu_ ha il pixel nell'immagine che ha coordinate x = 0, y = 0? Una volta ottenuti, applica quei valori al pixel con posizione x = 0 e y = 0 della finestra. Dopodiché, il ciclo for prosegue e analizzerà il pixel con coordinate x = 1 e y = 0 e avanti così.

Con l'**updatePixel()** finale aggiorniamo tutti i valori presenti nell'array della finestra. Il risultato finale sarà, dunque, vedere visualizzata sullo schermo l'immagine.

La domanda che sorge spontanea è: perché dovrei scrivere tutte queste righe di codice quando avrei potuto usare la funzione _image()_ e risparmiare un sacco di fatica? La risposta è semplice: avendo accesso ai dati grezzi dell'immagine possiamo modificarli a nostro piacimento.

Proviamo, ad esempio, ad aggiungere la riga in grassetto al nostro codice:

**r = constrain(r, 0, 100);**
 
pixels\[pos\] = color(r, g, b);

Il risultato sarà che il valore del _rosso_ non potrà avere un valore compreso tra 0 e 255 come previsto normalmente ma sarà limitato a valori compresi tra 0, 100 grazie alla funzione **constrain**.

![Processare le immagini in Processing](/assets/images/Processare-immagini-Processing-1024x912.png)

Siamo riusciti a creare il nostro primo filtro personalizzato per le immagini. Ora possiamo dare sfogo alla nostra fantasia.

Facciamo un altro esperimento: rimpiazziamo l'ultima riga di codice che abbiamo aggiunto con quella seguente:

r = map(mouseX, 0, width, 0, 255);

Il _rosso_ ora è controllato dalla posizione x del mouse.

## Usare un solo ciclo for

Prima di concludere questo post ci tengo a fare una precisazione: volendo è possibile utilizzare un solo ciclo for per ottenere lo stesso effetto riducendo, così, le righe di codice del nostro programma:

for(int i = 0; i < pixels.length; i++)

Se decidiamo di intraprendere questa strada dobbiamo eliminare la variabile _pos_ e sostituirla con _i_:

float r = red(img.pixels\[i\]);

Come avevamo discusso nel post relativo all'[array di pixel](https://blog.federicopepe.com/2017/03/array-pixel-loadpixels-updatepixels/) la differenza tra i due approcci dipende se consideriamo l'immagine un array monodimensionale o bidimensionale.
