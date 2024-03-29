---
title: "Esercizio: Testo psichedelico"
date: "2017-01-19"
categories: 
  - "processing-text"
coverImage: "Testo-Psichedelico-Animato_in_Processing.png"
---

Oggi vi propongo un esercizio molto semplice per analizzare alcune funzioni relative al testo che non abbiamo avuto modo di approfondire nei post precedenti. L'esercizio riportato qui sotto mostra come siano sufficienti poche righe di codice per ottenere risultanti interessanti lavorando con del testo all'interno di Processing.

Partiamo dal codice completo del programma:

```java
/*
 * Esercizio: Testo Psichedelico
 * Federico Pepe, 19.01.2017
 * http://blog.federicopepe.com/processing
*/
String letters = "";

void setup() {
  size(500, 500);
  background(255);
  fill(0);
  textSize(26);
  textAlign(CENTER);
}

void draw() {
  background(255);
  for(int i = 0; i <= letters.length(); i++) {
    if(i % 2 == 0) {
      fill(random(255), random(255), random(255));
    } else {
      fill(255);
    }
    text(letters, width/3 + i*1.5, height/2+i);
  }
}
 
void keyPressed() {
  if(key == BACKSPACE) {
    if (letters.length() > 0) {
      letters = letters.substring(0, letters.length()-1);
    }
  }
  else if(textWidth(letters+key) < width)  {
    letters = letters+key;
  }
}
```

L'intero programma si basa sulla variabile di tipo Stringa chiamata _letters_ che dichiariamo e inizializziamo nella prima riga.

## void keyPressed()

Di questa funziona-evento [abbiamo già parlato in passato](https://blog.federicopepe.com/2015/08/eventi-mousepressed-e-keypressed/). Sappiamo che il codice all'interno viene eseguito quando viene premuto un tasto della tastiera. Partiamo da un controllo condizionale per verificare se stiamo premendo il tasto backspace, quello che usiamo per cancellare l'ultimo carattere inserito.

Se la prima condizione è _true_ verifichiamo che la lunghezza della stringa sia maggiore di 0 `letters.length() > 0`. Se anche questa condizione risulta _true_ reimpostiamo il valore della variabile _letters_ eliminando l'ultimo carattere inserito: `letters = letters.substring(0, letters.length()-1);`.

Non avendo mai visto prima questi metodi delle variabili String, spiego velocemente come funzionano:

- **.length()** restituisce semplicemente il numero di caratteri della stringa.
- **.substring()** restituisce una nuova stringa che è parte della stringa iniziale. Accetta due parametri la posizione di partenza e quella finale.

Ritornando al primo if: se stiamo premendo un tasto e questo tasto non è backspace allora aggiungiamo il tasto premuto (`key`) alla nostra stringa a patto che la lunghezza della stringa non sia maggiore alla lunghezza della finestra del nostro sketch: `textWidth(letters+key) < width`

## Risultato

Quello che accade dentro setup() e draw() non dovrebbe essere troppo complesso da capire per cui, inserisco direttamente un'immagine che rappresenta un risultato ottenuto con questo sketch:

![Testo Psichedelico](/assets/images/Processing-Esercizio-Testo-Psichedelico.gif)
