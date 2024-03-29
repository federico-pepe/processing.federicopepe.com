---
title: "Coding Rescue #3 – Cambiare la tonalità di alcuni pixel"
date: "2018-01-21"
categories: 
  - "coding-rescue"
tags: 
  - "coding-rescue"
  - "loadpixels"
  - "processing"
---
# Coding Rescue #3 – Cambiare la tonalità di alcuni pixel

Negli ultimi giorni ho ricevuto diverse richieste di aiuto per problemi di codice in Processing; ecco la soluzione a uno dei problemi che mi sono stati posti.

Ho deciso di chiamare questo _Coding Rescue_: **cambiare la tonalità di alcuni pixel**.

## Il problema

Il quesito era piuttosto articolato:

- Il programma deve caricare un'immagine dal disco.
- Il programma decide se modificare o no il pixel in base ad un valore casuale.
- Il processo di trasformazione viene controllato dal click  del mouse: un primo click avvia la trasformazione che, con un successivo click, viene messa in pausa. Un ulteriore click fa ripartire la trasformazione e così via.
- I pixel devono essere modificati di continuo.
- Il compito deve essere svolto mediante la funzione _creaImmagine()_, che accetta in ingresso un oggetto di tipo **PImage** e rende in uscita un oggetto di tipo **PImage**, che sarà l’immagine modificata come da specifiche, e la funzione _calcolaPixel()_, che accetta in ingresso un oggetto di tipo **color** e rende in uscita un oggetto di tipo **color**, che sarà il pixel modificato come da specifiche.
- _creaImmagine()_ crea una nuova immagine utilizzando su ciascun pixel la funzione calcolaPixel().
- _calcolaPixel()_ calcola il nuovo pixel nel seguente modo: siano r, g, b i livelli di canale di un pixel. Sia _treshold_ un valore numerico posto inizialmente a 0.5. Sia _r_ un valore casuale compreso tra 0 e 1, generato per ogni pixel. Se _r>soglia_, allora la funzione lascia il pixel inalterato, in caso contrario il programma calcola i nuovi valori _rm_, _gm_, _bm_ (che definiscono il pixel modificato) nel seguente modo:
    - rm = 0.393∗r+0.769∗g+0.189∗b
    - gm = 0.349∗r+0.686∗g+0.168∗b
    - bm = 0.272∗r+0.534∗g+0.131∗bIn ogni caso i valori finali di r, g, b devono essere valori leciti, cioè compresi tra 0 e 255.
- Quando l'utente preme il tasto "+" la soglia viene incrementata di 0.1 mentre, con la pressione del tasto "-" la soglia viene decrementata di 0.1.

## La soluzione

```java

/*
 * Coding Rescue #3 - Cambiare la tonalità di alcuni pixel
 * Federico Pepe, 21.01.2018
 * http://blog.federicopepe.com/processing
 */

// Creo le variabili necessarie;
float threshold = 0.5;
boolean work = true;
PImage original, edited;

void setup() {
  // Nella funzione di setup carico il file dall'hard disk;
  size(1, 1);
  surface.setResizable(true);
  selectInput("Select a file to process:", "fileSelected");
}

void draw() {
  if (original != null) {
    edited = original.copy();
    /*
     * Se la variabile work, il cui valore dipende dal click del mouse è true, mostro
     * l'immagine originale, altrimenti avvio la modifica
     */
    if (work) {
      image(edited, 0, 0);
    } else {
      image(creaImmagine(edited), 0, 0);
    }
  }
}

// Funzione per gestire il caricamento dei file da HD
// https://processing.org/reference/selectInput_.html
void fileSelected(File selection) {
  if (selection == null) {
    println("Window was closed or the user hit cancel.");
  } else {
    println("User selected " + selection.getAbsolutePath());
    original = loadImage(selection.getAbsolutePath());
    surface.setSize(original.width, original.height);
  }
}

// Funzione creaImmagine che, come da specifiche, accetta in ingresso un oggetto PImage
// e restituisce un oggetto PImage;
PImage creaImmagine(PImage img) {
  // Carico i pixel in un array
  img.loadPixels();
  for (int y = 0; y < img.height; y++) {
    for (int x = 0; x < img.width; x++) {
      int loc = x + y * img.width;
      // Ottengo i valori R, G, B di ciascun pixel;
      float r = red(img.pixels[loc]);
      float g = green(img.pixels[loc]);
      float b = blue(img.pixels[loc]);
      // Lancio la funziona calcolaPixel
      img.pixels[loc] = calcolaPixel(color(r, g, b));
    }
  }
  img.updatePixels();
  return img;
}

color calcolaPixel(color c) {
  // Valore casuale, come da specifiche
  float r = random(0, 1);

  if (r > threshold) {
    // Se r è maggiore della soglia, restituisco il colore originale
    return c;
  } else {
    // Altrimenti calcolo il nuovo valore del pixel come richiesto
    // la funzione constrain mi assicura che il valore calcolato sia compreso tra 0 e 255;
    float rm = constrain(0.393*red(c)+0.769*green(c)+0.189*blue(c), 0, 255);
    float gm = constrain(0.349*red(c)+0.686*green(c)+0.168*blue(c), 0, 255);
    float bm = constrain(0.272*red(c)+0.534*green(c)+0.131*blue(c), 0, 255);
    // Restituisco i nuovi valori
    return color(rm, gm, bm);
  }
}

// Con la funzione keyPressed determino la pressione dei tasti + e -
void keyPressed() {
  if (key == '+') {
    threshold += 0.1;
  }
  if (key == '-') {
    threshold -= 0.1;
  }
  // Utilizzo la funzione round (di seguito) per arrotondare il valore a 2 decimali;
  round(threshold, 2);
}
// Alla pressione del mouse, cambio il valore di work da true a false e viceversa
void mouseClicked() {
  work = !work;
}
// Funzione utile per limitare il numero di decimali in un float
// https://stackoverflow.com/questions/9627182/how-do-i-limit-decimal-precision-in-processing
float round(float number, float decimal) {
  return (float)(round((number*pow(10, decimal))))/pow(10, decimal);
} 
```
