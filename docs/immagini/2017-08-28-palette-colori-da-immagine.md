---
title: "Una palette di colori da un'immagine"
date: "2017-08-28"
categories: 
  - "processing-images"
tags: 
  - "hex"
  - "pimage"
  - "savestrings"
  - "stringlist"
coverImage: "palette-colori-da-immagine-Processing.jpg"
---

Nelle ultime settimane mi è capitato di fare diversi lavori di grafica – che non è propriamente il campo in cui sono più ferrato – e mi sono sempre trovato in crisi nella scelta della palette di colori più adatta a quello che stavo facendo.

Mentre ero alla ricerca della giusta combinazioni di colori su siti come [Coolors](https://coolors.co) e [Adobe Color](https://color.adobe.com) mi è tornata in mente una frase di [Joshua Davis](http://joshuadavis.com) detta in uno dei suoi video (non cito testualmente, vado a memoria): le palette di colori che funzionano meglio sono quelle legate a immagini a cui siamo abituati, come un tramonto sul mare oppure le gradazioni di verde in un bosco in montagna. Ecco perché estrarre i colori da una foto è uno dei modi migliori per trovare delle combinazioni che funzionano.

Da qui l'illuminazione: perché non creare uno sketch in Processing per aiutarmi?

## Leggere i colori da un'immagine

Partiamo riciclando il codice visto nell'ultimo post: [Modificare la dimensione della finestra in base all'immagine caricata](https://blog.federicopepe.com/2017/06/modificare-la-dimensione-della-finestra-base-allimmagine-caricata/). Creiamo un oggetto di tipo **PImage** e facciamo in mondo che la finestra si ridimensioni automaticamente al caricamento del file. Nel codice sotto riportato noterete un +50 pixel nell'altezza che servirà come spazio per rappresentare i colori della palette in tempo reale.

Per questo sketch ho deciso di utilizzare l'immagine di un prato fiorito: [![Leggere i colori da un'immagine con Processing](/assets/images/flowers.jpg)](https://blog.federicopepe.com/wp-content/uploads/2017/08/flowers.jpg)

Ricordatevi di inserire l'immagine nella cartella _/data_ come spiegato [qui](https://blog.federicopepe.com/2017/03/utilizzare-immagini-in-processing/).

```java
/*
 * Una palette di colori da un'immagine
 * Federico Pepe, 28.08.2017
 * http://blog.federicopepe.com/processing
*/

PImage img;

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("flowers.jpg");
  surface.setSize(img.width, img.height+50); 
}

void draw() {
}
```

Creiamo due variabili di tipo integer: la prima, **numPoints** indica il numero di colori di cui sarà composta la nostra palette. Ho deciso di chiamarla _points_ perché prenderemo i dati colori da dei punti nell'immagine. La seconda **pointX** la utilizzeremo come riferimento per calcolare il valore di x dei punti scelti che, ai fini di questo esempio, saranno equidistanti.

Aggiungiamo un po' di codice nel ciclo draw(): mostriamo l'immagine come sfondo e carichiamo l'array di pixel. Come anticipato, assegniamo a pointX il valore della larghezza della foto caricata diviso il numero di punti.

Utilizziamo il classico ciclo for per trovare i colori dei punti. Creo un minimo di interfaccia per aiutarmi nel lavoro: intorno ai punti di riferimento disegno un cerchio.

```java
/*
 * Una palette di colori da un'immagine
 * Federico Pepe, 28.08.2017
 * http://blog.federicopepe.com/processing
*/

PImage img;
// Numero di "punti" della nostra palette
int numPoints = 5;
// Valore x di riferimento
int pointX;

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("flowers.jpg");
  surface.setSize(img.width, img.height+50); 
}

void draw() {
  image(img, 0, 0);
  img.loadPixels();
  pointX = img.width / numPoints;
  
  for(int i = 0; i <= numPoints-1; i++) {
    int x = pointX*i;
    int y = mouseY;
    
    if(mouseY <= 0 || mouseY >= img.height) {
      y = img.height/2;
    }
    stroke(255);
    noFill();
    ellipse(x, y, 25, 25);
    color c = img.pixels[x + y * img.width];
    println(c);
  }
  
}
```

Avendo deciso di lasciare il valore di y variabile e dipendente dalla posizione y del mouse, ho deciso di inserire un controllo condizionale per verificare di non uscire dall'immagine stessa causando un errore _Array out of bounds_ sull'array di pixel.

Nella console vengono mostrati i valori di c ma non sono utilizzabili in alcun programma di grafica perché non sono i classici valori HEX, RGB o HSB.

## Mostriamo la palette di colori

Sfrutto i 50 pixel di margine di abbondanza rispetto alla foto per mostrare in tempo reale i colori dei pixel di riferimento. Farlo è molto semplice: creo dei rettangoli con, come fill, il colore estratto in precedenza. Sfrutto questo passaggio per centrare i punti di analisi rispetto alla larghezza della finestra e ai rettangoli in basso.

[![Palette di colori da immagine](/assets/images/palette-di-colori-da-immagine-Processing-1024x741.png)](https://blog.federicopepe.com/wp-content/uploads/2017/08/palette-di-colori-da-immagine-Processing.png)

```java
/*
 * Una palette di colori da un'immagine
 * Federico Pepe, 28.08.2017
 * http://blog.federicopepe.com/processing
 */

PImage img;
// Numero di "punti" della nostra palette
int numPoints = 5;
// Valore x di riferimento
int pointX;

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("flowers.jpg");
  surface.setSize(img.width, img.height+50);
}

void draw() {
  image(img, 0, 0);
  img.loadPixels();
  pointX = img.width / numPoints;

  for (int i = 0; i <= numPoints-1; i++) {
    int x = pointX/2+pointX*i;
    int y = mouseY;

    if (mouseY <= 0 || mouseY >= img.height) {
      y = img.height/2;
    }

    stroke(255);
    noFill();
    ellipse(x, y, 25, 25);

    color c = img.pixels[x + y * img.width];

    fill(c);
    rect(pointX*i, img.height, pointX, 50);
  }
}
```

## Otteniamo i valori HEX dei colori

A questo punto il programma funziona nel modo corretto, non ci resta che fare dei piccoli miglioramenti all'interfaccia: grazie alla funzione **hex(value, digits)** possiamo ottenere il valore esadecimale del colore. Come indicato nel [reference](https://processing.org/reference/hex_.html), il numero viene rappresentato con un massimo di 8 caratteri ma possiamo ottenerne 6, come siamo abituati, aggiungendo indicando il secondo parametro alla funzione.

![Palette colori GIF](/assets/images/palette-colori-hex-1.gif)

Ecco qui il codice:

```java
/*
 * Una palette di colori da un'immagine
 * Federico Pepe, 28.08.2017
 * http://blog.federicopepe.com/processing
 */

PImage img;
// Numero di "punti" della nostra palette
int numPoints = 5;
// Valore x di riferimento
int pointX;

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("flowers.jpg");
  surface.setSize(img.width, img.height+50);
}

void draw() {
  image(img, 0, 0);
  img.loadPixels();
  pointX = img.width / numPoints;

  for (int i = 0; i <= numPoints-1; i++) {
    int x = pointX/2+pointX*i;
    int y = mouseY;

    if (mouseY <= 0 || mouseY >= img.height) {
      y = img.height/2;
    }

    stroke(255);
    noFill();
    ellipse(x, y, 25, 25);

    color c = img.pixels[x + y * img.width];

    fill(c);
    rect(pointX*i, img.height, pointX, 50);
    
    fill(255);
    textAlign(CENTER);
    text("#"+hex(c,6), x, img.height+30);
    
  }
}
```

## Salvare la palette di colori in un file di testo

Siamo quasi alla fine del nostro lavoro: l'unico passaggio che ci manca è salvare la palette di colori in un file .txt in modo da poterli usare a nostro piacimento anche in programmi esterni.

Aggiungiamo qualche riga di codice: creiamo una nuova variabile di tipo **StringList** il cui contenuto verrà inizializzato a ogni ciclo di draw con la funzione .clear();

Alla pressione del tasto del mouse, verrà salvato il file chiamato palette.txt. La conversione della StringList in array è necessaria perché la funzione **saveStrings** si aspetta come secondo parametro un array e non una lista.

```java
/*
 * Una palette di colori da un'immagine
 * Federico Pepe, 28.08.2017
 * http://blog.federicopepe.com/processing
 */

PImage img;
// Numero di "punti" della nostra palette
int numPoints = 5;
// Valore x di riferimento
int pointX;
// Salviamo i valori HEX in una lista di stringhe
StringList palette = new StringList();

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("flowers.jpg");
  surface.setSize(img.width, img.height+50);
}

void draw() {
  image(img, 0, 0);
  
  img.loadPixels();
  pointX = img.width / numPoints;
  
  palette.clear();
  
  for (int i = 0; i <= numPoints-1; i++) {
    int x = pointX/2+pointX*i;
    int y = mouseY;

    if (mouseY <= 0 || mouseY >= img.height) {
      y = img.height/2;
    }

    stroke(255);
    noFill();
    ellipse(x, y, 25, 25);

    color c = img.pixels[x + y * img.width];

    fill(c);
    rect(pointX*i, img.height, pointX, 50);
    
    fill(255);
    textAlign(CENTER);
    text("#"+hex(c,6), x, img.height+30);
    // Aggiungiamo il colore come stringa all'array
    palette.append("#"+hex(c,6));
    
  }
}

void mousePressed() {
  saveStrings("palette.txt", palette.array());
}
```
