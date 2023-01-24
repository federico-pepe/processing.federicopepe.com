# Array di oggetti: Bouncing Ball, parte 4

È finalmente arrivato il momento di mettere insieme quanto imparato nell'ultimo mese, [programmazione ad oggetti](https://blog.federicopepe.com/2016/01/introduzione-agli-oggetti/) e [array](https://blog.federicopepe.com/2016/01/array/), e di concludere il nostro esercizio **Bouncing Ball**. La domanda a cui oggi daremo, finalmente, risposta è sempre la stessa: _come faccio a creare decine o centinaia di oggetti_?

## Un array di oggetti

Riprendiamo il codice dell'esercizio Bouncing Ball dove l'[avevamo lasciato](https://blog.federicopepe.com/2016/01/esercizio-bouncing-ball-parte-3-oop/). Il primo passo è dichiarare un array di oggetti di tipo Ball.

La prima riga del nostro programma serviva per dichiarare una variabile di tipo **Ball** (il nostro oggetto) di nome _myBall._

`Ball myBall;`

Sostituiamo questa riga di codice con un array di oggetti: per mantenere il mio codice chiaro e leggibile modifico anche il nome della variabile da myBall (che identifica un oggetto solo) a _myBalls_, utilizzando il plurale.

`Ball[] myBalls;`

Nella funzione _setup()_ dove, precedentemente, inizializzavo l'oggetto ora devo dichiarare grandezza del mio array. Decido di avere a disposizione 100 oggetti:

`myBalls = new Ball[100];`

Non mi resta che inizializzare tutti gli oggetti richiamando il constructor all'interno della nostra classe, per sveltire, utilizzo un ciclo for:

for(int i = 0; i < myBalls.length; i++) {
 myBalls\[i\] = new Ball(random(width), random(height), random(0.5 ,5), random(0.5, 5));
 }

## Debugging di un array di oggetti

Con l'ultima porzione di codice abbiamo riempito il nostro array occupando tutte e 100 le caselle con 100 oggetti differenti assegnando a ciascuno di essi, grazie alle funzioni random, la posizione X e Y e la velocità sull'asse orizzontale e verticale.

Se volessimo essere sicuri di averlo fatto nel modo corretto, potremmo pensare di utilizzare, come abbiamo sempre fatto finora, la funzione _println(myBalls);_

![Debugging an Array in Processing](/assets/images/Array_Debugging-1024x898.png)

Come potete vedere nell'immagine, il testo riportato nella console non è per niente chiaro. Trattandosi di un array, proviamo a sostituire _println_ con _printArray_:

![Processing: using printArray](/assets/images/Processing_printArray-1024x898.png)

Un risultato leggermente migliore: vediamo che ci sono effettivamente 100 oggetti, numerati da 0 a 99, ma facciamo ancora fatica a capire se il contenuto del nostro array è corretto.

## Accedere alle variabili interne agli oggetti

Nei nostri esercizi relativi agli oggetti abbiamo imparato a usare la _dot notation_ per richiamare i metodi all'interno degli oggetti. La riga di codice myBall.display() serviva per richiamare la funzione _display()_ contenuta nell'oggetto creato precedentemente.

Utilizzando lo stesso metodo possiamo accedere anche alle variabili interne all'oggetto: scrivendo, ad esempio, _myBall.ellipseX;_ verrà restituito il valore di ellipseX.

Dal momento che, però, non stiamo lavorando con un singolo oggetto ma con un array abbiamo due possibilità:

1. accedere ai dati di un oggetto specifico: _println(myBalls\[34\].ellipseX);_
2. utilizzare la variabile contatore nel nostro ciclo for per visualizzarli tutti

Aggiungiamo questa riga di codice all'interno del nostro ciclo for:

`println("["+i+"] - ellipseX: " + myBalls[i].ellipseX);`

Ed ecco che il risultato è finalmente comprensibile:

![Processing accessing variables in objects](/assets/images/Processing_accessing-variables-inside-objects-1024x898.png)

## Bouncing Balls, parte 4

Concludiamo modificando il codice contenuto in _draw()_ per vedere tutte e cento le nostre sfere rimbalzare sullo schermo.

```java
Ball[] myBalls;

void setup() {
  size(700, 500);
  myBalls = new Ball[100];
  for(int i = 0; i < myBalls.length; i++) {
    myBalls[i] = new Ball(random(width), random(height), random(0.5 ,5), random(0.5, 5));
  }  
}

void draw() {
  background(0);
  for(int i = 0; i < myBalls.length; i++) {
    myBalls[i].display();
    myBalls[i].move();
    myBalls[i].checkEdges();
  } 
}
```

Non ho incluso il codice della classe Ball perché non è stata toccata nemmeno una riga di codice. Se avete fatto tutto correttamente, il risultato sarà il seguente:

[![Bouncing Ball Final](/assets/images/Processing_Bouncing_Ball_final.gif)](https://blog.federicopepe.com/wp-content/uploads/2016/01/Processing_Bouncing_Ball_final.gif)
