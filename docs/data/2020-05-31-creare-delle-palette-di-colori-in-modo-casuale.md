---
title: "Creare delle palette di colori che stanno bene insieme in modo casuale"
date: "2020-05-31"
categories: 
  - "colors"
  - "processing"
tags: 
  - "colormode"
  - "hsb"
  - "palette"
  - "processing"
coverImage: "000336-palette.png"
---

Un paio di giorni fa su Twitter ho seguito un piccolo thread partito da **[Vegard Myklebust](https://twitter.com/usefulslug)** che spiegava come creare delle palette di colori che funzionano bene insieme in modo del tutto casuale.

Il sistema è davvero semplice e, dopo aver fatto qualche esperimento, posso dire che funziona ottimamente. Ho pensato che potesse valere la pena di realizzare un piccolo programma in Processing per generare palette di colori al bisogno.

https://twitter.com/usefulslug/status/1265604318016811011

Il [thread originale](https://twitter.com/usefulslug/status/1265604318016811011) su Twitter

## Regole per creare una palette

Queste sono le regole da seguire per creare la palette di colori:

1. Non lavorare in uno spazio [colore RGB](https://blog.federicopepe.com/2015/08/colori-rgb/) (_red, green and blue)_, meno intuitivo per le persone, ma in HSB (_hue, saturation and brightness)_.
2. La chiave di tutto sta nel valore di **hue**, ovvero la scelta del colore. Se consideriamo i valori possibili di hue su una circonferenza i suoi valori andranno da 0 a 360. 
    Scegliamone un valore in modo del tutto casuale.
3. Scegliere in modo del tutto casuale anche i valori di _saturation_ e _brightness_.
4. Ora abbiamo ottenuto il nostro primo colore, quello posizionato al centro della palette.
5. Scegliamo un altro valore numerico in modo del tutto casuale. Il sistema funziona al meglio se questo nuovo valore è compreso tra 0 e 180. Sommiamo e sottraiamo questo valore al valore di _hue_ scelto precedentemente.
6. In questo modo abbiamo ottenuto i due colori da posizionare accanto a quello centrale.
7. Ripetiamo l'operazione al punto 5 sommando e sottraendo nuovamente il valore scelto in quel punto a entrambi i colori ottenuti precedentemente.
8. Per ottenere i risultati migliori, assegnare in modo casuale _saturation_ e _brightness_ a tutti i colori.

## Il programma in Processing

```java
/*
 * Create a palette of 5 random colours with a techniques explained
 * here https://twitter.com/usefulslug/status/1265604318016811011
 *
 * Sketch made by Federico Pepe
 * http://www.federicopepe.com
 * 27.05.2020
 *
*/

color palette[] = new color[5];

void setup() {
  size(540, 540);
  
  colorMode(HSB, 360, 100, 100);
  
  noStroke();
  
  createPalette();
  drawPalette();
}

void draw() {
}

void mousePressed() {
  background(0);
  createPalette();
  drawPalette();
}

void keyPressed() {
  if(key == 's') {
    saveFrame("######-palette.png");
  }
}

void createPalette() {
  int hue = round(random(360));
  int r1  = round(random(180));
  palette[0] = color(hue - (r1*2), round(random(100)), round(random(100)));
  palette[1] = color(hue - r1, round(random(100)), round(random(100)));
  palette[2] = color(hue, round(random(100)), round(random(100)));
  palette[3] = color(hue + r1, round(random(100)), round(random(100)));
  palette[4] = color(hue + (r1*2), round(random(100)), round(random(100)));
  
  println("#" + hex(palette[0], 6), 
    "#" + hex(palette[1], 6), 
    "#" + hex(palette[2], 6), 
    "#" + hex(palette[3], 6), 
    "#" + hex(palette[4], 6));
  
}

void drawPalette() {
  fill(palette[0]);
  rect(0, 0, width/5, height);
  fill(palette[1]);
  rect(width/5, 0, width/5, height);
  fill(palette[2]);
  rect(width/5*2, 0, width/5, height);
  fill(palette[3]);
  rect(width/5*3, 0, width/5, height);
  fill(palette[4]);
  rect(width/5*4, 0, width/5, height);
}
```

Il programma è molto semplice: ho creato due funzioni personalizzate _createPalette()_ e _drawPalette()_ per gestire al meglio la creazione e la rappresentazione a schermo delle palette.

I colori vengono salvati in un array nominato _palette_ per comodità.

Ad ogni click del mouse viene generata una nuova palette mentre, premendo il tasto **s** sulla tastiera, viene salvata un'immagine nella cartella del programma.

In console è possibile vedere i valori esadecimali dei colori ottenuti richiamando la funzione _hex()_ sui dati di tipo _color_ all'interno dell'array.

Ecco qualche esempio:

[![](images/000322-palette.png)](https://i1.wp.com/blog.federicopepe.com/wp-content/uploads/2020/05/000605-palette.png?ssl=1&resize=540%2C540)

[![](https://i1.wp.com/blog.federicopepe.com/wp-content/uploads/2020/05/001011-palette.png?ssl=1&resize=540%2C540)](https://i1.wp.com/blog.federicopepe.com/wp-content/uploads/2020/05/001011-palette.png?ssl=1&resize=540%2C540)
