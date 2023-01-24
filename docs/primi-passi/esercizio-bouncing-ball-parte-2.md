# Esercizio: Bouncing Ball, parte 2

Prima di procedere con la lettura di questo post, assicuratevi di aver letto la prima parte: [Esercizio: Bouncing Ball, parte 1](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-1/). Avete provato a trovare la soluzione al quesito posto alla fine dell'articolo?

## Bouncing Ball

Eravamo rimasti con un cerchio che, una volta disegnato sullo schermo, si muoveva da destra verso sinistra e, una volta raggiunto il bordo, invertiva il suo moto tornando indietro. Una volta raggiunto il bordo destro, però, proseguiva il suo moto sparendo dalla nostra vista.

Per fare in modo che il cerchio rimbalzi avanti e indietro, è sufficiente aggiungere una semplice condizione:

if(ellipseX > width || ellipseX < 0)

Ecco quindi il codice completo:

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
  if(ellipseX > width || ellipseX < 0) {
    speedX = speedX * -1;
  }
  ellipseX = ellipseX + speedX;
  println("EllipseX: " + ellipseX + " SpeedX: " + speedX);
}
```

## Aggiungiamo anche l'asse verticale

Ora che la nostra "palla" si muove solo sull'asse X, implementiamo il movimento anche sull'asse verticale. La variabile ellipseY è già presente nel nostro codice, dobbiamo solo creare una nuova variabile speedY e ricopiare parte del codice modificando solo i parametri necessari:

```java
int ellipseX;
int ellipseY;
int speedX = 1;
int speedY = 1;

void setup() {
  size(700, 500);
  ellipseX = 0;
  ellipseY = height/2;
}

void draw() {
  background(0);
  ellipse(ellipseX, ellipseY, 50, 50);
  if(ellipseX > width || ellipseX < 0) {
    speedX = speedX * -1;
  }
  if(ellipseY > height || ellipseY < 0) {
    speedY = speedY * -1;
  }
  ellipseX = ellipseX + speedX;
  ellipseY = ellipseY + speedY;
  //println("EllipseX: " + ellipseX + " SpeedX: " + speedX);
}
```

Utilizzando delle variabili per controllare la velocità, variando un numero possiamo modificare l'andamento della nostra palla. Se assegniamo a speedX o speedY un valore iniziale di 5, il cerchio si muoverà molto più velocemente.

Eliminando _background(0)_ all'inizio del blocco di codice draw(), potrete tenere monitorato il movimento della vostra palla sullo schermo, come mostrato nell'immagine qui sotto:

![Bouncing ball: eliminiamo background(0) dalla funzione draw()](/assets/images/Bouncing_ball-1024x800.png)

A questo punto il nostro _sketch_ è pronto per essere migliorato utilizzando funzioni e oggetti; nel prossimo post scopriremo come rendere il nostro codice modulare.
