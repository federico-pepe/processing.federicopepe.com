# Esercizio: Bouncing Ball, parte 3 (OOP)

Se vi siete persi gli articoli precedenti, qui trovate la [parte 1](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-1/) e la [parte 2](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-parte-2/) di questo esercizio. Con questo post non aggiungeremo niente di nuovo al nostro programma ma rivedremo per intero il codice per trasformarlo in una versione ad oggetti.

## Bouncing Ball Object Oriented

Per prima cosa aggiungiamo una nuova Tab che chiameremo _Ball_, come la classe che creeremo:
```
class Ball {
 
}
```
Per non dimenticarci il constructor, aggiungiamo subito la sintassi necessaria:
```
class Ball {
 Ball() {
 }
}
```
A questo punto facciamo copia-incolla delle porzioni di codice che, nel nostro sketch principale, riguardano la nostra palla: ricordatevi di portare nella classe sia le variabili che le funzioni.

Questo è il risultato finale:

```java
class Ball {
  int ellipseX;
  int ellipseY;
  int speedX;
  int speedY;

  Ball() {
    ellipseX = 0;
    ellipseY = height/2;
    speedX = 1;
    speedY = 1;
  }

  void display() {
    ellipse(ellipseX, ellipseY, 50, 50);
  }

  void move() {
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
}
```

```java
Ball myBall;

void setup() {
  size(700, 500);
  myBall = new Ball();
}

void draw() {
  background(0);
  myBall.display();
  myBall.move();
  myBall.checkEdges();
}
```

## Aggiungiamo constructor

Miglioriamo la nostra classe creando dei nuovi constructor a cui possiamo passare delle variabili. Come già fatto nell'esempio del post precedente, conviene sostituire il _data type_ delle variabili da _integer_ a _float_.

```java
class Ball {
  // VARIABILI
  float ellipseX;
  float ellipseY;
  float speedX;
  float speedY;
  
  // CONSTRUCTOR
  Ball() {
    ellipseX = random(width);
    ellipseY = random(height);
    speedX = 1;
    speedY = 1;
  }
  
  Ball(float _ellipseX) {
    ellipseX = _ellipseX;
    ellipseY = random(height);
    speedX = 1;
    speedY = 1;
  }
  
  Ball(float _ellipseX, float _ellipseY) {
    ellipseX = _ellipseX;
    ellipseY = _ellipseY;
    speedX = 1;
    speedY = 1;
  }
  
  Ball(float _ellipseX, float _ellipseY, float _speedX) {
    ellipseX = _ellipseX;
    ellipseY = _ellipseY;
    speedX = _speedX;
    speedY = 1;
  }
  
  Ball(float _ellipseX, float _ellipseY, float _speedX, float _speedY) {
    ellipseX = _ellipseX;
    ellipseY = _ellipseY;
    speedX = _speedX;
    speedY = _speedY;
  }
  
  // METODI
  void display() {
    ellipse(ellipseX, ellipseY, 50, 50);
  }

  void move() {
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
}
```

A questo punto non ci resta che sperimentare se funziona tutto correttamente provando a passare delle variabili alla nostra classe:

`myBall = new Ball(random(width), random(height), 5, 10);`
