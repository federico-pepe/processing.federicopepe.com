# Interazione tra oggetti

Dopo la parentesi sugli array ([parte 1](https://blog.federicopepe.com/2016/01/array/), [parte 2](https://blog.federicopepe.com/2016/01/array-di-oggetti/)), torniamo a parlare di oggetti. Una domanda che può sorgere spontanea è: possono due oggetti interagire tra loro?

Riprendendo porzioni di codice che già abbiamo usato in precedenza oggi realizzeremo uno sketch in cui sarà presente un'interazione tra due oggetti: cambieremo il colore dello sfondo da nero a rosso quando due cerchi si sovrapporranno uno all'altro.

## Analizziamo il problema

Come posso sapere se due cerchi si intersecano? Per crearli in Processing utilizziamo la funzione _ellipse()_ che accetta quattro parametri: posizione x e y del centro più la larghezza e l'altezza. Nel caso in cui questi ultimi due parametri coincidano avrò un cerchio.

Grazie agli studi fatti alle scuole elementari e medie sappiamo che esiste una cosa chiamata raggio che determina la distanza tra il centro e il bordo del cerchio. A questo punto, la soluzione al problema dovrebbe esservi chiara: se la distanza tra il centro del primo cerchio e del secondo è inferiore alla somma dei due raggi, allora i cerchi saranno sovrapposti, altrimenti no.

Se avete dimenticato la geometria, questa immagine dovrebbe esservi d'aiuto per visualizzare quello che ho appena scritto:

![Cerchi sovrapposti](/assets/images/Processing_Interazione_Cerchi.jpg)

## Punto di partenza: copia-incolla

Ora che abbiamo individuato il fulcro del nostro programma, faccio copia-incolla del codice dall'esercizio _[Bouncing Ball](https://blog.federicopepe.com/2016/01/array-di-oggetti/)_, semplificandolo in alcune parti: all'interno della mia classe "Ball" utilizzerò un solo constructor a cui passerò solo il valore relativo al raggio del cerchio. Posizione x e y del centro e velocità di spostamento saranno creati in modo casuale.

Mantengo inalterato il metodo _display()_ mentre modifico leggermente il metodo _move()_ nel quale inserisco anche la parte di codice relativa al controllo sui bordi.

Nel programma principale creo e inizializzo due oggetti di tipo Ball chiamati myBall1 e myBall2 e, all'interno di draw() li visualizzo e li faccio muovere:

```java
class Ball {
  // Variabili
  int radius;
  float ellipseX, ellipseY, speedX, speedY;
  // Constructor
  Ball(int _radius) {
    radius = _radius;
    ellipseX = random(width);
    ellipseY = random(height);
    speedX = random(2, 5);
    speedY = random(2, 5);
  }
  // Metodi
  void display() {
    ellipse(ellipseX, ellipseY, radius, radius);
  }
  
  void move() {
    ellipseX = ellipseX + speedX;
    ellipseY = ellipseY + speedY;
    if (ellipseX > width || ellipseX < 0) {
      speedX = speedX * -1;
    }
    if (ellipseY > height || ellipseY < 0) {
      speedY = speedY * -1;
    }
  }
}
```

```java
Ball myBall1, myBall2;

void setup() {
  size(700, 500);
  myBall1 = new Ball(100);
  myBall2 = new Ball(50);
}

void draw() {
  background(0);
  myBall1.display();
  myBall2.display();
  myBall1.move();
  myBall2.move();
}
```

## Determinare la sovrapposizione

Ora non mi resta che creare un nuovo metodo all'interno della classe per verificare l'effettiva sovrapposizione dei due cerchi. Il primo passo che potremmo pensare di fare è creare una funzione in cui utilizziamo sei parametri (posizione x, y e raggio dei due cerchi) per verificare l'intersezione dei due cerchi.

Dal momento che utilizziamo gli oggetti, possiamo arrivare a una soluzione più semplice: **l'oggetto myBall1 interseca myBall2**?

Aggiungiamo un metodo alla nostra classe: il tipo di dato che verrà restituito da questo nuovo metodo sarà di tipo _[booleano](https://blog.federicopepe.com/2015/11/controlli-condizionali-iii-variabili-booleane/)_ (_true_ in caso di sovrapposizione e _false_ in caso contrario) per cui scriviamo quanto segue:

boolean isOver() {

}

Per calcolare la distanza tra due punti utilizziamo la funzione _[dist()](https://processing.org/reference/dist_.html)_ che accetta quattro parametri e restituisce un dato di tipo _float:_

`dist(x1, y1, x2, y2);`

Chiaramente i primi due parametri saranno ellipseX ed ellipseY del cerchio che stiamo prendendo in esame. Ma come facciamo a passare i dati del secondo cerchio? Nel [secondo post relativo agli oggetti](https://blog.federicopepe.com/2016/01/oop-classi-e-oggetti-parte-2/) abbiamo visto come passare dei parametri all'interno del costructor, possiamo usare lo stesso sistema per passare delle variabili anche ai metodi.

La cosa davvero interessante è che anziché passare una variabile, passeremo l'intero oggetto:

boolean isOver(Ball b) {
 float distance = dist(ellipseX, ellipseY, b.ellipseX, b.ellipseY);
 if(distance <= (radius+b.radius)) {
  return true;
 } else {
  return false;
 }
}

Ecco il codice completo della classe Ball:

```java
class Ball {
  
  int radius;
  float ellipseX, ellipseY, speedX, speedY;
  
  Ball(int _radius) {
    radius = _radius;
    ellipseX = random(width);
    ellipseY = random(height);
    speedX = random(2, 5);
    speedY = random(2, 5);
  }
  
  void display() {
    ellipse(ellipseX, ellipseY, radius, radius);
  }
  
  void move() {
    ellipseX = ellipseX + speedX;
    ellipseY = ellipseY + speedY;
    if (ellipseX > width || ellipseX < 0) {
      speedX = speedX * -1;
    }
    if (ellipseY > height || ellipseY < 0) {
      speedY = speedY * -1;
    }
  }
  
  boolean isOver(Ball b) {
    float distance = dist(ellipseX, ellipseY, b.ellipseX, b.ellipseY);
    if(distance <= (radius+b.radius)) {
      return true;
    } else {
      return false;
    }
  }
}
```

## Interazione tra due oggetti

Aggiorniamo il codice dello sketch principale aggiungendo all'interno di draw le seguenti righe di codice:

if(myBall2.isOver(myBall1)) {
 background(255, 0, 0);
}

Ed il gioco è fatto.

## Trova l'errore

Anziché lasciarvi con un esercizio, questa volta ho un'altra sfida per voi. Il nostro programma funziona ma c'è un piccolo errore che non lo fa funzionare esattamente come ci eravamo prefissati. Sapete individuarlo?

Per aiutarvi allego un'immagine:

![Trova l'errore](/assets/images/Processing_trova_lerrore-1024x800.png)
