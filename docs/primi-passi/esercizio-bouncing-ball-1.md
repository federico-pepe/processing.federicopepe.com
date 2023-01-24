# Esercizio: Bouncing Ball, parte 1

Con il post di oggi, cominciamo a lavorare a un classico problema di programmazione che raccoglie gran parte delle nozioni viste finora. L'evoluzione di questo esercizio comprenderà, ovviamente, l'utilizzo di funzioni personalizzate e ci servirà per cominciare a parlare di programmazione orientata agli oggetti.

## Punto di partenza

Il nostro obiettivo è scrivere un programma in cui faremo muovere un cerchio all'interno della finestra. Una volta raggiunto un bordo, il nostro cerchio non dovrà fermarsi o "sparire" uscendo dallo spazio a nostra disposizione ma dovrà invertire la direzione del suo movimento.

Per comodità e per seguire un **modello di sviluppo** coerente, suddividerò il nostro obiettivo in problemi più semplici che affronterò uno alla volta facendo riferimento ai post in cui abbiamo già trattato problemi simili.

## Disegniamo il cerchio e facciamolo muovere in una direzione

Questa è la parte più semplice: ricordate il post [Variabili in Processing: operazioni matematiche](https://blog.federicopepe.com/2015/09/variabili-in-processing-ii-operazioni-matematiche/)?

A differenza dell'esempio sopra citato, creiamo uno sketch con due variabili: ellipseX e ellipseY che utilizzeremo per determinare la posizione del cerchio nella finestra.

```java
int ellipseX;
int ellipseY;

void setup() {
  size(700, 500);
  ellipseX = 0;
  ellipseY = height/2;
}

void draw() {
  background(0);
  ellipse(ellipseX, ellipseY, 50, 50);
  ellipseX++;
}
```

Il programma funziona correttamente: il cerchio si muove da sinistra verso destra. L'unico problema è che una volta raggiunto il bordo destro, la variabile _ellipseX_ continua ad aumentare il suo valore di 1 fino a far scomparire il cerchio. Attenzione: il nostro cerchio è sparito dalla finestra ma, anche se noi non lo vediamo, sta proseguendo il suo movimento verso destra.

## Abbiamo raggiunto il bordo?

```java
int ellipseX;
int ellipseY;

void setup() {
  size(700, 500);
  ellipseX = 0;
  ellipseY = height/2;
}

void draw() {
  background(0);
  ellipse(ellipseX, ellipseY, 50, 50);
  if(ellipseX < width) {
    ellipseX++;
  }
}
```

Inseriamo un semplice [controllo condizionale](https://blog.federicopepe.com/2015/09/controlli-condizionali-if-else-if-else/): se ellipseX è minore della larghezza della finestra aumentiamo la variabile. Quando ellipseX sarà uguale a 700, in questo caso specifico, il cerchio si fermerà.

## Invertiamo la direzione del movimento

A questo punto dobbiamo invertire la direzione del movimento. Normalmente si è portati a pensare a una cosa del genere:

```java
int ellipseX;
int ellipseY;

void setup() {
  size(700, 500);
  ellipseX = 0;
  ellipseY = height/2;
}

void draw() {
  background(0);
  ellipse(ellipseX, ellipseY, 50, 50);
  if(ellipseX < width) {
    ellipseX++;
  } else {
    ellipseX--;
  }
}
```

Se avviate questo sketch vi accorgerete, però, che il cerchio non torna indietro. Com'è possibile? Analizziamo i valori che assume la variabile ellipseX: [ricordatevi](https://blog.federicopepe.com/2015/09/println-e-random/) che è sempre possibile inserire _println();_ per fare il [debugging](https://blog.federicopepe.com/2015/09/variabili-in-processing-ii-operazioni-matematiche/).

Cliccando su Run, il valore di ellipseX è uguale a 0. A ogni ciclo draw() ellipseX viene aumentato di 1 quindi la variabile assumerà i valori, 1, 2, 3 ecc... fino ad arrivare a 700. Chiaramente a ogni ciclo viene effettuato il controllo if: se ellipseX è minore della variabile width (che ha valore 700) allora verrà aggiunto 1.

Quando ellipseX assume il valore 700, la condizione if(ellipseX < width) sarà _false_ e scatterà il blocco di codice presente nell'else e quindi a ellipseX verrà assegnato un valore di 699. Al ciclo successivo il controllo if(ellipseX < width) sarà di nuovo _true_ e quindi alla variabile verrà sommato 1 e tornerà a un valore di 700.

Questo si ripeterà all'infinito e la variabile assumerà solo valori pari a 699 o 700 bloccando, di fatto, il movimento del cerchio.

Per invertire la direzione del movimento dobbiamo fare qualcosa in più: aggiungere una variabile per controllare la direzione dello spostamento a cui invertiremo il segno (da positivo a negativo) per far si che il cerchio torni effettivamente indietro.

Per cambiare il segno di un numero da positivo a negativo sappiamo che è sufficiente moltiplicarlo per -1. Mi rendo conto che, spiegandolo a parole, questo passaggio è un po' complicato; per aiutarvi nella comprensione ho inserito un println() alla fine del codice per mostrare in console i valori di ellipseX e speedX.

Altra puntualizzazione: ho modificato anche il controllo condizionale da _if(ellipseX < width)_ a _if(ellipseX > width)_ per far funzionare il programma correttamente e cambiare il segno solo al raggiungimento del bordo destro.

```java
int ellipseX;
int ellipseY;
int speedX = 1;

void setup() {
  size(700, 500);
  ellipseX = 0;
  ellipseY = height/2;
}

void draw() {
  background(0);
  ellipse(ellipseX, ellipseY, 50, 50);
  if(ellipseX > width) {
    speedX = speedX * -1;
  }
  ellipseX = ellipseX + speedX;
  println("EllipseX: " + ellipseX + " SpeedX: " + speedX);
}
```

Il nostro cerchio ora torna indietro ma, una volta raggiunto il bordo sinistro, scompare nuovamente dalla finestra.

Ora tocca a voi dimostrare di aver capito come procedere: dovete fare in modo che il cerchio torni indietro una volta raggiunto anche il bordo sinistro e poi, ovviamente, implementare lo stesso procedimento anche sull'asse verticale. La soluzione sarà pubblicata nella seconda parte!
