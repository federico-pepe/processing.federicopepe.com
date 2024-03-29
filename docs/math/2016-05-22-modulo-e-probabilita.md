---
title: "Modulo e probabilità"
date: "2016-05-22"
categories: 
  - "processing-math"
tags: 
  - "framecount"
  - "framerate"
  - "modulo"
  - "probabilita"
coverImage: "Processing_3.png"
---

L'ultima volta che abbiamo [parlato di operatori matematici](https://blog.federicopepe.com/2015/09/variabili-in-processing-ii-operazioni-matematiche/) è stato un po' di tempo fa. Prima di procedere con nuovi argomenti, però, è necessario studiare ancora un paio di cose legate al mondo della matematica: con il post di oggi approfondiremo l'operatore **modulo** e scopriremo come effettuare un semplice **calcolo di probabilità** nei nostri sketch.

## Modulo

L'operatore modulo – che viene indicato dal simbolo di percentuale **%** – si trova in tutti i linguaggi di programmazione e ci aiuta a esprimere una funzione matematica molto semplice che conosciamo da quando studiamo le divisioni alle elementari: il calcolo del resto.

Possiamo utilizzare questo operatore sia con numeri o variabili di tipo _integer_ o _float_:

println(10/5);
println(10%5);

Queste due linee di codice mostreranno nella console due risultati differenti: la prima, infatti, è una normale divisione: 10 diviso 5 restituisce 2. La seconda linea restituirà 0 perché la divisione non ha resto.

println(11/5);
println(11%5);

In questo secondo esempio, invece, la prima riga di codice ci restituirà ancora 2 mentre la seconda darà come risultato 1.

Perché l'operatore modulo è utile ai fini della programmazione? La risposta è abbastanza semplice: se usato in combinazione con il controllo del **frame rate** – ovvero il numero di volte al secondo che la funzione _draw()_ ridisegna lo schermo – possiamo dare un ritmo al nostro programma.

## frameRate() e frameCount

La funzione **frameRate()** posizionata all'interno di _setup()_ imposta il numero di frame per secondo (fps) a cui girerà il nostro programma. Ricordo che di default Processing lavora a 60fps. Richiamando la variabile di sistema **frameCount**, invece, ci verrà restituito il numero di frame che sono trascorsi dall'avvio del programma.

```java
/*
 * Esempio dell'utilizzo di frameRate() e frameCount.
 * In questo esempio, imposto il programma affinché giri a 30fps
 * e visualizzo in console il numero di frame che sono trascorsi
 * dall'avvio.
*/
void setup() {
  frameRate(30);
}

void draw() {
  println(frameCount);
}
```

Mettiamo insieme quanto visto finora e facciamo in modo che il colore di sfondo del nostro sketch cambi ogni 30 frame (ovvero ogni secondo).

```java
 /*
 * Modulo, frameRate e frameCount
 * In questo programma impostiamo il frameRate a 30fps
 * e cambiamo colore di sfondo una volta ogni secondo.
*/

void setup() {
  frameRate(30);
}

void draw() {
  if(frameCount%30 == 0) {
    background(255, 0, 0);
  } else {
    background(255);
  }
}
Sign up for free 
```

Se volessimo modificare il programma in modo che il cambio avvenga ogni 2 secondi, sarebbe sufficiente modificare la riga numero 12 così: `if(frameCount%60 == 0)`

## Probabilità

In programmazione e, in particolare, quando si tratta di _creative coding_, può essere utile implementare un semplice **calcolo di probabilità** per stabilire quando far eseguire una certa porzione di codice. Come si fa a stabilire quante possibilità ci sono che un dato evento avvenga? Bisogna dividere il numero di volte che una cosa possa accadere per il numero totale di probabilità.

Quindi, per fare un esempio, quante possibilità abbiamo che lanciando una moneta esca testa? Su una moneta ci sono due facce: una testa e una croce, quindi 1/2 = 50%.

Per simulare un sistema casuale ci aiutiamo con la funzione **random()**, di cui abbiamo già [parlato in passato](https://blog.federicopepe.com/2015/09/println-e-random/). Modifico il programma precedente facendo sì che il cambio di colore di sfondo avvenga con una probabilità del 20%:

```java
/*
 * Calcolo delle probabilità
*/

void setup() {
  frameRate(30);
}

void draw() {
  float prob = 0.2;
  float random = random(1);
  if(random < prob) {
    background(255, 0, 0);
  } else {
    background(255);
  }
}
```
