# Variabili in Processing II: operazioni matematiche

Con il post [della settimana scorsa](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/), la vostra vita da programmatori ha subìto un cambiamento radicale: imparare a utilizzare le variabili è un notevole passo avanti che apre scenari inediti.

## Aumentare il valore delle variabili

Il mio obiettivo per questo primo esempio è di disegnare un cerchio che, partendo da una posizione predefinita, si muova verso destra.

Vi ricordo che la funzione _ellipse()_ [accetta quattro parametri](https://blog.federicopepe.com/2015/07/primitive-2d-point-line-rect-ellipse-triangle/): posizione x e y di origine, larghezza e altezza dell'ellisse. Dunque, di quante variabili avrò bisogno? Siccome ho deciso di far muovere il mio cerchio da sinistra verso destra sull'asse x, la risposta è molto semplice: una soltanto che chiamerò **ellipseX**.

Il tipo di dato di cui avrò bisogno sarà sicuramente numerico ma dovrò utilizzare un numero intero (_integer_) o decimale (_float_)? Tecnicamente potrei usare entrambi ma, dal momento che i pixel non sono suddivisibile, utilizzerò un **integer**.

Ultimo problema: come faccio ad aumentare il valore della variabile? Visto che il blocco di codice draw() viene eseguito ripetutamente dal programma, sarà sufficiente fare un'addizione all'interno di esso.

Per aumentare il valore della variabile di 1 ogni ciclo, abbiamo tre diverse possibilità:

`ellipseX = ellipseX + 1;`

`ellipseX += 1;`

`ellipseX ++;`

Il risultato che otteniamo è sempre lo stesso; l'unico caso in cui c'è una reale differenza tra le tre linee di codice sopra elencate è se volessimo aumentare la variabile di un valore diverso da 1 a ogni ciclo; in tal caso non potremmo usare il terzo modo ma dovremmo scrivere:

`ellipseX = ellipseX + 2;`

`ellipseX += 2;`

Ecco, dunque, il codice del nostro primo esempio:

```java
/*
 * Utilizzo delle variabili II: Esempio 1
 * by Federico Pepe
 * http://blog.federicopepe.com
 */

int ellipseX; // dichiarazione della variabile

void setup() {
  size(540, 540);
  ellipseX = 0; // inizializzazione
  
}

void draw() {
  background(255);
  ellipse(ellipseX, height/2, 50, 50);
  ellipseX = ellipseX + 1; // aumento il valore di ellipseX
}
```

Se vi state chiedendo come mai la funzione _background()_ sia in _draw()_, consiglio di [rileggere questo post](https://blog.federicopepe.com/2015/08/blocchi-di-codice-e-flusso-setup-e-draw/).

Questo è il risultato:

![Aumento della variabile ellipseX](/assets/images/Processing_utilizzo_variabili_esempio_14.gif)

**Attenzione:** Per comodità ho creato una gif animata che viene riprodotta in loop; con il codice sopra indicato, una volta che il cerchio esce dallo schermo a dx, non ricompare al suo punto di partenza sulla sinistra.

## Operazioni matematiche con le variabili

Abbiamo visto come effettuare una somma, per le altre operazioni matematiche, il codice è simile:

### Sottrazione:

```
ellipseX = ellipseX - 1;

ellipseX -= 1;

ellipseX --;
```

### Moltiplicazione:

```
ellipseX = ellipseX * 2;

ellipseX *= 2
```

### Divisione:

```
ellipseX = ellipseX / 2;

ellipseX /= 2;
```

Nel caso della moltiplicazione e della divisione è molto improbabile trovare esempi di codice che utilizzano il secondo metodo.

## Debugging delle variabili: println();

Quando si comincia a lavorare con le variabili, una delle funzioni più utili da imparare è _println()_. Essa ci permette di tenere costantemente monitorato il valore che assumono le variabili che stiamo utilizzando attraverso la console di debugging.

Aggiungiamo questa nuova funzione nel nostro esempio di prima:

```java
/*
 * Utilizzo delle variabili II: Esempio 2
 * by Federico Pepe
 * http://blog.federicopepe.com
 */

int ellipseX; // dichiarazione della variabile

void setup() {
  size(540, 540);
  ellipseX = 0; // inizializzazione
  
}

void draw() {
  background(255);
  ellipse(ellipseX, height/2, 50, 50);
  ellipseX = ellipseX + 1; // aumento il valore di ellipseX
  println(ellipseX);
}
```

![Debugging variabili in Processing](/assets/images/Variabili_Processing_println-880x1024.png)

Sulla funzione println() faremo un breve approfondimento in futuro perché, essendo una delle funzioni che utilizzeremo di più, è importante che sia chiaro il suo funzionamento; nel frattempo sbizzarritevi a creare sketch animati utilizzando le variabili.
