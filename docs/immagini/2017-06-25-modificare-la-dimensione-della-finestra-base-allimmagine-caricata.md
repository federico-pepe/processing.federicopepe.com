---
title: "Modificare la dimensione della finestra in base all'immagine caricata"
date: "2017-06-25"
categories: 
  - "processing-images"
tags: 
  - "setup"
  - "size"
  - "surface-setresizable"
  - "surface-setsize"
coverImage: "Processing_3_new_editor.png"
---

Negli esempi che abbiamo visto fino ad ora relativi all'uso delle immagini all'interno di Processing abbiamo sempre impostato a priori la grandezza della finestra del nostro sketch in base alla dimensione dell'immagine caricata.

È un metodo molto semplice ma decisamente scomodo se dobbiamo utilizzare tante immagini diverse oppure se vogliamo rendere il nostro programma universale.

Nella versione precedente di Processing era possibile utilizzare delle variabili all'interno della funzione _size()_. Questa opzione, però, benché fortemente osteggiata dagli sviluppatori fin dal 2009 è stata definitivamente rimossa con l'aggiornamento a Processing 3 perché impediva miglioramenti in termini di performance, velocità e compatibilità cross-platform.

Non disperate! Esiste una soluzione alternativa che, però, non è ben descritta nel _reference_ del linguaggio. Ecco perché ho pensato fosse interessante scrivere un breve articolo a riguardo.

Ecco come fare:

- All'interno di _setup()_ è comunque necessario indicare una dimensione di partenza con la funzione _size()_. Per semplicità possiamo scrivere: size(1, 1);
- Dopodiché aggiungiamo la seguente linea di codice: `surface.setResizable(true);` mi raccomando, fate attenzione alle maiuscole!
- A questo punto, nel punto in cui abbiamo la necessità di reimpostare la dimensione è sufficiente scrivere: `surface.setSize(larghezza, altezza);` dove _larghezza_ e _altezza_ sono i nostri parametri.

Ecco un esempio con un'immagine:

```java
/*
 * Modificare la dimensione della finestra in base all'immagine caricata
 * Federico Pepe, 25.06.2017
 * http://blog.federicopepe.com/processing
*/

PImage img;

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("immagine.jpg");
  surface.setSize(img.width, img.height);  
}

void draw() {
}
```

Per cambiare la dimensione a ogni click del mouse:

```java
/*
 * Modificare la dimensione della finestra in base all'immagine caricata
 * Federico Pepe, 25.06.2017
 * http://blog.federicopepe.com/processing
*/

void setup() {
  size(100, 100);
  surface.setResizable(true);
}

void draw() {
}

void mousePressed() {
  surface.setSize(round(random(100, 500)), round(random(100, 500)));  
}
```
