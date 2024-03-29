---
title: "Coding Rescue #2 - Binarizza un'immagine"
date: "2017-10-26"
categories: 
  - "coding-rescue"
coverImage: "binarizza_Processing-Coding-Rescue.png"
---
# Coding Rescue #2 - Binarizza un'immagine

Secondo capitolo della rubrica [Coding Rescue](https://blog.federicopepe.com/category/coding-rescue/) dove provo a risolvere i vostri problemi con Processing. Questa volta la consegna è piuttosto articolata, riassumo i punti salienti:

- Lo scopo del programma è quello di "binarizzare" un'immagine ovvero fare in modo che, al click del mouse, i colori dell'immagine vengano modificati utilizzando la funzione **binarize()**. La funzione imposta un _pixel bianco_ se la sua luminosità è maggiore di una soglia impostata e _nero se inferiore_.
- per calcolare la luminosità, si deve utilizzare la funzione **brightness()**.
- impostare la soglia iniziale a un valore predefinito (a scelta) ma implementare una funzione **calculateThreshold()** con cui ricalcolarla dinamicamente utilizzando al distanza percorsa dal mouse tra due frame successivi.

## Binarizza un'immagine, la soluzione

![binarizza un'immagine con Processing](/assets/images/binarizza_Processing-Coding-Rescue-1024x852.png)

Ecco qui il codice:

```java

/*
 * Coding Rescue #2 - Binarizzare un'immagine
 * Federico Pepe, 26.10.2017
 * http://blog.federicopepe.com/processing
 */
float threshold = 150;
PImage immagine, imgbin;
boolean bin = true;

void setup() {
  size(700, 542);
  immagine = loadImage("corgi-photo.jpg");
  image(immagine, 0, 0);
  frameRate(2);
} 

void draw() {
  threshold = calculateThreshold();
  if (bin) {
    imgbin = immagine.copy();
    image(binarize(imgbin), 0, 0);
  } else {
    image(immagine, 0, 0);
  }
}

void mouseClicked() {
  bin = !bin;
}  

PImage binarize(PImage img) {
  img.loadPixels();
  for (int y = 0; y < img.height; y++) {
    for (int x = 0; x < img.width; x++) { int loc = x + y * img.width; if (brightness(img.pixels[loc]) > threshold) {
        img.pixels[loc] = color(0);
      } else {
        img.pixels[loc] = color(255);
      }
    }
  }
  img.updatePixels();
  return img;
}

float calculateThreshold() {
  float d = dist(pmouseX, pmouseY, mouseX, mouseY);
  threshold = d;
  return threshold;
}
```
