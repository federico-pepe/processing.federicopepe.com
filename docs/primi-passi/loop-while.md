# Loop: while

Grazie ai controlli condizionali, abbiamo imparato come risolvere un importante problema: fare in modo che il nostro programma rispetti una logica eseguendo alcune porzioni di codice solo al verificarsi di determinate condizioni. Ora, però, ci troviamo di fronte a un'altra questione importante per il nostro futuro da programmatori: siamo in grado di disegnare qualcosa sullo schermo una volta ma non sappiamo come ripetere, in modo semplice e veloce, più volte la stessa figura sullo schermo.

Ovviamente possiamo fare copia-incolla della nostra funzione, ad esempio ellipse(), modificare qualche parametro affinché le figure non si sovrappongano una all'altra ma questo non è certamente il modo migliore di procedere. Provate a pensare, infatti, cosa succederebbe se volessimo disegnare 500 cerchi: sarebbe complicato tenere il conto del numero esatto di copie. Se, poi, ci accorgessimo di voler fare una piccola modifica probabilmente ci passerebbe la voglia di cambiare 500 righe di codice.

Introduciamo oggi il concetto di _loop_.

## Loop

Lo scopo del loop è, per l'appunto, racchiudere in un blocco di codice delle istruzioni che devono essere ripetute un esatto numero di volte. Esistono fondamentalmente due tipologie di loop: _while_ e _for_. In questo post ci concentreremo di più sul primo anche se, lo ammetto, io preferisco di gran lunga utilizzare i cicli for. Nel prossimo post, quando li approfondiremo, scoprirete anche il perché.

## While

Concettualmente i cicli di loop sono molto simili ai controlli condizionali:

```
if(condizione) {
 // Blocco di codice
}
```

Abbiamo imparato che, in un if, il blocco di codice viene eseguito **quando** la condizione inserita tra le parentesi è vera.

```
while(condizione) {
 // Blocco di codice
}
```

Nel loop while, il blocco di codice verrà eseguito **finché** la condizione inserita tra le parentesi è vera.

## Esempio pratico

Come al solito facciamo subito un esempio e analizziamo il codice che ha generato l'immagine:

![While loop in Processing](/assets/images/Processing_loop_while-1024x800.png)

```java
int y = 10;

void setup() {
  size(700, 500);
  background(255);
  while(y < height) {
    line(100, y, 600, y);
    y += 10;
  }
}

void draw() {
}
```

Lo scopo di questo programma è disegnare delle linee orizzontali distanziate di 10 pixel l'una dall'altra fino al raggiungimento dell'altezza della finestra.

Come potete vedere nel codice, all'inizio abbiamo dichiarato e inizializzato la variabile, chiamata y, che utilizzeremo per verificare la condizione all'interno del ciclo while. In _setup()_ abbiamo impostato la grandezza della finestra e il colore dello sfondo e poi abbiamo inserito il nostro loop:

_finché_ il valore della variabile y sarà inferiore all'altezza della finestra, disegna una linea orizzontale le cui coordinate saranno: 100, y, 600, y. Aumenta poi il valore di y di 10.

Quando il codice viene eseguito il programma lo analizza in questo modo:

- Il valore iniziale di y è 10 (valore con cui abbiamo inizializzato la variabile all'inizio del programma), y è minore dell'altezza della finestra (500px)? Si, allora disegna una linea con le seguenti coordinate: 100, 10, 600, 10. y = 10+10;
- y = 20. y è minore di 500? Si, allora disegna una linea con le coordinate: 100, 20, 600, 20. y = 20+10;
- y = 30. y è minore di 500? Si, allora disegna una linea con le coordinate: 100, 30, 600, 30. y = 30+10;
- y = 40. y è minore di 500? Si, allora disegna una linea con le coordinate: 100, 40, 600, 40. y = 40+10;
- ...
- y = 490. y è minore di 500? Si, allora disegna una linea con le coordinate: 100, 490, 600, 490. y = 490+10;
- y = 500. y è minore di 500? No, allora esci dal ciclo while.

Provate a pensare a quanto tempo avremmo perso a disegnare quelle righe una alla volta e, soprattutto, nel caso in cui volessimo modificare la distanza tra le linee da 10 a 5 pixel, ci basta modificare un singolo parametro: y += 5.

## Attenzione!

Ecco alcune cose importanti che dobbiamo tenere a mente quando utilizziamo un ciclo loop di tipo while:

- Abbiamo bisogno di creare una variabile da utilizzare come "**contatore**" per verificare se la condizione è _true_.
- Il valore della variabile contatore **deve** essere modificato all'**interno** del ciclo while.
- Bisogna fare attenzione che ci sia una **condizione di uscita** dal loop altrimenti il ciclo si ripeterà all'infinito mandando in blocco il computer.
