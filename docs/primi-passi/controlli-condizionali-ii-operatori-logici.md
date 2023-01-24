# Controlli Condizionali: operatori logici

La [scorsa settimana](/primi-passi/controlli-condizionali-if-else-if-else/) abbiamo imparato a utilizzare i controlli condizionali **if**, **else if** ed **else** per fare in modo che i nostri programmi eseguano determinate azioni al verificarsi di condizioni prestabilite.

## Operatori Logici

Oggi approfondiamo l'argomento introducendo gli **Operatori Logici**. Può capitare, infatti, di avere la necessità di concatenare insieme più controlli condizionali: immaginiamo, ad esempio, di voler realizzare un programma in cui il colore dello sfondo cambia in base sia alla posizione X che Y del mouse.

In italiano dovremmo scrivere una cosa simile a:

**SE** la posizione X del mouse è inferiore alla metà della larghezza della finestra **E** la posizione Y del mouse è inferiore alla metà dell'altezza della finestra **ALLORA** colora lo sfondo di nero.

Possiamo tradurre in codice la frase di prima così:

```java
void setup() {
  size(500, 500);
}

void draw() {
  if(mouseX < width/2) {
    if(mouseY < height/2 {
    }
  }
}
```

Oppure, in modo più elegante:

```java
void setup() {
  size(500, 500);
}

void draw() {
  if((mouseX < width/2) && (mouseY < height/2)) {
  }
}
```

Gli operatori logici che possiamo utilizzare sono fondamentalmente 3:

- **_&&_** (AND) quando entrambe le condizioni devono essere _true_
- **||** (OR) quando è sufficiente che una delle due condizioni sia _true_
- **!** (NOT) per testare se la condizione è _not true_ oppure _not false_

Faccio una precisazione: benché non sia richiesto, se non in casi particolari, che le condizioni prima e dopo l'operatore logico siano racchiuse tra parentesi, io preferisco sempre aggiungere delle parentesi tonde per essere sicuro di rendere chiaro quali condizioni sto testando.

Ecco un esempio:

```java
void setup() {
  size(500, 500);
  stroke(255);
}

void draw() {
  if((mouseX < width/2) && (mouseY < height/2)) {
    background(255, 0, 0);
  } else if((mouseX > width/2) && (mouseY < height/2)) {
    background(0, 255, 0);
  } else {
    background(0);
  }
  line(width/2, 0, width/2, height);
  line(0, height/2, width, height/2);
}
```

Traduco il codice in italiano:

Imposto una finestra di dimensioni 500x500px e che le linee di riferimento disegnate saranno di colore bianco. **SE** la posizione X del mouse sarà inferiore alla metà della larghezza della finestra **E** la posizione Y del mouse sarà inferiore alla metà dell'altezza della finestra allora lo sfondo sarà rosso **ALTRIMENTI SE** la posizione X del mouse sarà superiore alla metà della larghezza della finestra E la posizione Y del mouse sarà inferiore alla metà dell'altezza della finestra allora lo sfondo sarà verde **ALTRIMENTI** lo sfondo sarà nero.

Questo è il risultato:

[![Utilizzo degli operatori Logici in Processing](/assets/images/Operatori-Logici-in-Processing-2-1024x587.jpg)](https://blog.federicopepe.com/wp-content/uploads/2015/10/Operatori-Logici-in-Processing-2.jpg)

[![Utilizzo degli operatori logici in Processing](/assets/images/Operatori-Logici-in-Processing-1024x587.jpg)](https://blog.federicopepe.com/wp-content/uploads/2015/10/Operatori-Logici-in-Processing.jpg)

## Compiti per casa

Prendendo spunto dal codice che abbiamo scritto oggi, scrivete un programma in cui la finestra, con lo sfondo di colore nero, sia divisa in 4 quadranti (consiglio di fare delle linee di riferimento di colore bianco). L'obiettivo del vostro programma è fare in modo che si evidenzi con il colore bianco il quadrante su cui passate sopra con il mouse facendo in modo che gli altri 3 rimangono di colore nero.

Buon lavoro!
