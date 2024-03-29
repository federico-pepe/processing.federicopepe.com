---
title: "Utilizzare immagini in Processing: PImage, loadimage() e image()"
date: "2017-03-12"
categories: 
  - "processing-images"
tags: 
  - "image"
  - "immagini"
  - "loadimage"
  - "pimage"
coverImage: "Processing_PImage_Sketch_Folder.png"
---

In tutti gli sketch che abbiamo creato fino a oggi abbiamo sempre utilizzato Processing per generare forme sullo schermo. Con questo post, invece, cominceremo ad ampliare i nostri orizzonti e inizieremo a utilizzare nei nostri programmi immagini esterne.

A differenza dei programmi di editing più comuni – penso per esempio a Photoshop o Pixelmator – con Processing possiamo lavorare in modo più preciso e dettagliato su ogni singola foto andando a regolare, a nostro piacimento, ogni pixel.

## Le immagini sono dati

Le immagini digitali non sono altro che un insieme di dati, ovvero numeri. Per cercare di spiegarlo nel modo più semplice possibile, ciascun dato rappresenta i valori di [rosso, verde e blu](https://blog.federicopepe.com/2015/08/colori-rgb/) (RGB) di un punto preciso all'interno di una griglia.

Di fatto possiamo immaginare ogni foto come una griglia di pixel dove ciascun pixel avrà diversi valori di rosso, verde e blu. Con la programmazione e un po' di fantasia possiamo avere accesso a tutti questi dati e usarli a nostro piacimento.

## PImage, loadImage() e image()

Abbiamo già parlato di [tipi di dati](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/) e [classi](https://blog.federicopepe.com/2016/01/oop-sintassi-di-classi-e-oggetti/). Processing ha al suo interno la classe **PImage** la cui funzione principale è quella di permetterci di caricare e visualizzare un'immagine.

La funzione **loadImage()**, che accetta un parametro di tipo _String_, carica il file all'interno della memoria. Nell'esempio riportato in seguito, il parametro passato alla funzione è il nome del file comprensivo di estensione. La funzione andrà a cercare se quel file è presente all'interno della sottocartella _data_ presente all'interno del nostro sketch.

Per chi non lo ricordasse, [in questo post](https://blog.federicopepe.com/2016/12/caricare-file-esterni-processing/) abbiamo già trattato come caricare file esterni all'interno del nostro sketch in Processing.

Mettiamo tutto insieme:

```java
/*
 * Utilizzare immagini in Processing: PImage, loadimage() e image()
 * Federico Pepe, 12.03.2017
 * http://blog.federicopepe.com/processing
*/

PImage immagine;

void setup() {
  size(500, 500);
  immagine = loadImage("logo_federicopepe.png");
}

void draw() {
  image(immagine, 0, 0);
}
```

Ho creato una variabile di tipo **PImage** chiamata _immagine_; attraverso la funzione **loadImage()** carico il file chiamato _logo\_federicopepe.png_ che, in precedenza, avevo già spostato all'interno della cartella _data_ e, infine, con la funzione **image()** visualizzo l'immagine facendo in modo che il bordo in alto a sinistra corrisponda alle coordinate 0, 0.

Ecco il risultato:

[![loadImage(), image() e PImage](/assets/images/Processing_PImage_Immagini-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2017/03/Processing_PImage_Immagini.png)

L'immagine viene visualizzata correttamente perché il file originale è di 500 x 500 pixel. Per completezza condivido anche lo screenshot della cartella dello sketch.

[![La cartella dello sketch che contiene l'immagine](/assets/images/Processing_PImage_Sketch_Folder-1024x636.png)](https://blog.federicopepe.com/wp-content/uploads/2017/03/Processing_PImage_Sketch_Folder.png)

Processing accetta i seguenti tipi di file: _GIF, JPG, TGA_ e _PNG._

## Un paio di precisazioni

Abbiamo detto che **PImage** è una classe. Perché non abbiamo mai chiamato un _constructor_ per inizializzarla? La funzione **loadImage()** in questo caso ha la funzione del constructor restituendo una nuova istanza dell'oggetto PImage generata dal file che carichiamo.

Se quest'ultima frase vi sembra arabo, consiglio di ripassare i post dedicati alla programmazione ad oggetti:

- [Introduzione agli oggetti](https://blog.federicopepe.com/2016/01/introduzione-agli-oggetti/)
- [OOP: Sintassi di classi e oggetti](https://blog.federicopepe.com/2016/01/oop-sintassi-di-classi-e-oggetti/)
- [OOP: Classi e oggetti, parte 2](https://blog.federicopepe.com/2016/01/oop-classi-e-oggetti-parte-2/)

Come illustrato nel _reference_ la funzione **image()** richiede un minimo di tre parametri: immagine da caricare, posizione x e y. È possibile passare alla funzione due parametri ulteriori per specificare la larghezza e l'altezza dell'immagine: un metodo comodo e veloce per ridimensionare le foto:

```java
/*
 * Utilizzare immagini in Processing: PImage, loadimage() e image()
 * Federico Pepe, 12.03.2017
 * http://blog.federicopepe.com/processing
*/

PImage immagine;

void setup() {
  size(500, 500);
  immagine = loadImage("logo_federicopepe.png");
}

void draw() {
  // Utilizzo due parametri aggiuntivi per ridimensionare la foto
  image(immagine, 0, 0, 100, 100);
}
```

[![Immagine ridimensionata](/assets/images/Processing-ridimensionare-immagine-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2017/03/Processing-ridimensionare-immagine.png)
