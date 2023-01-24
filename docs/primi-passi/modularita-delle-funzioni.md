# Modularità delle funzioni

Proseguiamo la nostra esplorazione nel mondo delle [funzioni personalizzate](https://blog.federicopepe.com/2015/11/funzioni-personalizzate/) e rendiamo lo sketch che abbiamo realizzato con l'esercizio _Bouncing Ball ([parte 1](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-1/), [parte 2](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-parte-2/))_ modulare.

Per diventare dei buoni programmatori è necessario lavorare costantemente alla riscrittura del proprio codice: è un processo continuo di riorganizzazione e ottimizzazione.

Riprendiamo il codice a cui eravamo arrivati con l'ultimo esercizio:

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

## Divisione in  moduli

In quanti moduli possiamo suddividere il nostro programma? Rileggiamo il codice e analizziamo ogni porzione di codice:

- Righe 1 - 4: dichiarazione delle variabili
- Righe 6- 10: configurazione generale con la funzione _setup()_
- Righe 13-14: disegniamo la nostra palla
- Righe 15-20: controlliamo che la palla non vada oltre i bordi della finestra e, se necessario, invertiamo la direzione del movimento.
- Righe 21-22: facciamo muovere la nostra palla

Chiaramente i primi due punti non possono essere modificati: le variabili devono funzionare in vari punti del nostro programma quindi sono [pubbliche](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/#scopo-variabili) mentre la parte di configurazione è già all'interno della funzione _setup()_.

Gli altri 3 punti, invece, sono tutti all'interno della funzione _draw()_ ma si occupano di tre attività differenti: disegnare, controllare e muovere la palla. Creiamo un modulo per ciascuna di esse.

Ricordo che non dovendo restituire nessun valore, utilizzeremo la parola **void** e che possiamo nominare ciascuna funzione come preferiamo purché non si utilizzino parole già riservate.

La funzione _drawBall()_ sarà quella dedicata al disegno della palla

```java
void drawBall() {
 background(0);
 ellipse(ellipseX, ellipseY, 50, 50);
}
```

 _moveBall()_ si occuperà del movimento

```java
void moveBall() {
 ellipseX = ellipseX + speedX;
 ellipseY = ellipseY + speedY;
}
```

E infine _checkEdges()_ verificherà se la palla ha raggiunto un bordo

```java
void checkEdges() {
 if (ellipseX > width || ellipseX < 0) {
 speedX = speedX * -1;
 }
 if (ellipseY > height || ellipseY < 0) {
 speedY = speedY * -1;
 }
}
```

## Bouncing Ball: modulare

Ecco il codice riscritto:

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
  drawBall();
  checkEdges();
  moveBall();
}

void drawBall() {
  background(0);
  ellipse(ellipseX, ellipseY, 50, 50);
}

void moveBall() {
  ellipseX = ellipseX + speedX;
  ellipseY = ellipseY + speedY;
}

void checkEdges() {
  if (ellipseX > width || ellipseX < 0) {
    speedX = speedX * -1;
  }
  if (ellipseY > height || ellipseY < 0) {
    speedY = speedY * -1;
  }
}
```

Se clicchiamo su _Run_ non noteremo alcuna differenza di funzionamento tra questo codice e quello incollato a inizio post.

Qualcuno potrebbe giustamente notare che, però, siamo passati da 24 linee di codice a 34: ben 10 righe di codice in più senza aver, di fatto, cambiato nulla nel funzionamento del nostro programma. Di contro, però, il nostro codice è più pulito e leggibile.

Il reale miglioramento si capirà quando, con il prossimo post, cominceremo a parlare di oggetti.
