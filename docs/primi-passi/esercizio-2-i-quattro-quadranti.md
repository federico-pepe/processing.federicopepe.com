# Esercizio 2: I quattro quadranti

Nell'ultima lezione pubblicata abbiamo parlato di controlli condizionali e operatori logici. Ecco la soluzione all'esercizio dei "quattro quadranti":

```java
/*
 *  Esercizio 2: I quattro quadranti
 *  by Federico Pepe
 *  http://blog.federicopepe.com/processing
 */
 
 void setup() {
   size(500, 500);
   stroke(255);
   fill(255);
 }
 
 void draw() {
   // Imposto il colore nero di background
   background(0);
   
   // Verifico la posizione X e Y del mouse e disegno il rettangolo
   // nel quadrante in cui si trova il mouse
   if(mouseX < width/2 && mouseY < height/2) {
     rect(0, 0, width/2, height/2);
   } else if(mouseX > width/2 && mouseY < height/2) {
     rect(width/2, 0, width/2, height/2);
   } else if(mouseX < width/2 && mouseY > height/2) {
     rect(0, height/2, width/2, height/2);
   } else {
     rect(width/2, height/2, width/2, height/2);
   }
   // Disegno le linee di riferimento
   line(width/2, 0, width/2, height);
   line(0, height/2, width, height/2);
 }
```

Le linee di codice sembrano molte ma, in realtà, la logica è piuttosto semplice. Nella parte di _setup()_ imposto la grandezza della finestra e alcuni parametri di base: il colore delle linee di riferimento e il fill sarà bianco.

All'interno di _draw()_ verifico la posizione X e Y del mouse all'interno di una serie di controlli condizionali. Traduco in pseudocodice la condizione che vado a controllare nel primo _if_: se la posizione X del mouse ha un valore minore della metà della larghezza della finestra **e** la posizione Y del mouse ha un valore minore della metà dell'altezza della finestra allora disegnerò un rettangolo il cui punto di partenza sia l'angolo in alto a sinistra, ovvero il punto con coordinate 0, 0 e le cui dimensioni siano la metà della finestra sia in larghezza che in altezza.

Negli else if successivi verifico le altre condizioni e disegno il quadrato bianco di conseguenza. Nell'ultimo else non occorre porre nessuna condizione perché è, per esclusione, l'ultima possibilità ovvero che il mouse si trovi nel quadrante in basso a destra.

Perché utilizzo delle variabili invece di parametri hard-coded? Avrei potuto benissimo scrivere:

`if(mouseX < 250 && mouseY < 250)`

In tal caso, però, il codice funzionerebbe correttamente solo nel caso in cui le dimensioni della mia finestra siano impostate, come nell'esempio, a 500 x 500 pixel. Con le variabili, posso modificare i parametri in size e avere un programma sempre funzionante.
