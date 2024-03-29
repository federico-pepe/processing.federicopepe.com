---
title: "Altri esempi con la funzione noise()"
date: "2016-07-07"
categories: 
  - "processing-math"
tags: 
  - "beginshape"
  - "endshape"
  - "noise"
  - "vertex"
coverImage: "Processing_noise_graph_animated.gif"
---

Nell'ultimo post abbiamo analizzato la differenza tra la funzione _random()_ e _noise()_. La prima, vi ricordo, restituisce dei valori assolutamente casuali che dipendono dai parametri che passiamo alla funzione; la seconda, invece, ci permette di avere una sorta di _casualità controllata_.

I valori che vengono restituiti dalla funzione _noise()_ hanno due caratteristiche fondamentali: sono correlati tra loro e hanno sempre un valore compreso tra 0 e 1.

Maggiore sarà la vicinanza tra i parametri che passiamo alla funzione, maggiore sarà, ovviamente, la correlazione tra i valori restituiti in output. È possibile verificare quanto ho appena detto utilizzando un paio di righe di codice:

println(noise(100));
println(noise(100.01));

Questo il risultato visualizzato in console:

0.3187103
0.318551

I risultati sono davvero molto vicini tra loro. Proviamo ad aumentare la distanza tra i due valori:

println(noise(100));
println(noise(101));

Ora la correlazione tra i due output è meno evidente:

0.56860673
0.48344862

Aumentando ulterioremente la distanza tra i parametri di input, avremo risultati in output sempre più simili a quelli ottenuti dalla funzione random():

println("Noise:");
println(noise(100));
println(noise(500));
println("Random:");
println(random(1));
println(random(1));

Può generare risultati simili a questo:

Noise:
0.16914257
0.68422705
Random:
0.48342746
0.89731866

## Creare un grafico di valori restituiti da noise()

Il primo esempio che voglio realizzare oggi è un grafico che mi rappresenti, per valori di x crescenti, un valore y restituito da noise().

Ecco il codice:

```java
/*
 * Noise examples 1
 * by Federico Pepe
*/

float xoff = 0;
float increment = 0.02;

void setup() {
  size(500, 500);
  background(255);
  noFill();
  noLoop();
}

void draw() {
  beginShape();
  for(int x = 0; x <= width; x++) {
    stroke(0);
    vertex(x, noise(xoff)*height);
    xoff += increment;
  }
  endShape();
}
```

Analizziamo velocemente il codice riportato qui sopra: per prima cosa creo le variabile di tipo float **xoff** e **increment**, dopodiché all'interno di _setup()_ imposto la grandezza della finestra, il colore di sfondo, imposto che non ci sia nessun colore di riempimento, con _noFill()_, e che il programma non vada in loo  una volta avviato, con _noLoop()_.

In _draw()_ utilizzo una funzione che non abbiamo ancora visto: [**beginShape()**](https://processing.org/reference/beginShape_.html). Questa funzione dice a Processing che vogliamo disegnare una forma complessa che avrà un'insieme di vertici – aggiunti con la funzione [**vertex()**](https://processing.org/reference/vertex_.html) – che dovranno essere uniti in ordine gli uni agli altri finché non chiuderemo la forma con [**endShape()**](https://processing.org/reference/endShape_.html).

Perché ho deciso di usare questa funzione? Perché così, estraendo per valori di x crescenti dei valori y generati dalla funzione _noise(),_ tutti i punti saranno già collegati tra loro e genereranno un grafico come quello rappresentato qui sotto:

![Grafico della funzione noise](/assets/images/Processing_noise_graph-988x1024.png)

## Animiamo il grafico

```java
/*
 * Noise example 2
 * by Federico Pepe
*/

float xoff;
float increment = 0.015;
float startPoint;

void setup() {
  size(500, 500);
  background(255);
  noFill();
}

void draw() {
  background(255);
  xoff = startPoint;
  beginShape();
  for(int x = 0; x <= width; x++) {
    stroke(0);
    vertex(x, noise(xoff)*height);
    xoff += increment;
  }
  endShape();
  startPoint += increment;
}
```

Con una veloce modifica al codice è possibile animare il grafico: per prima cosa eliminiamo il _noLoop()_ e aggiungiamo una variabile per stabilire di volta in volta quale sarà il nostro punto di inizio: **startPoint**. Ovviamente, al termine del loop, dobbiamo incrementare quest'ultima variabile in modo da avere lo scorrimento orizzontale.

Ecco il risultato (in formato gif):

![Grafico noise animato](/assets/images/Processing_noise_graph_animated.gif)
