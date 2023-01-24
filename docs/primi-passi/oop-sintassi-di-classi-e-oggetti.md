# OOP: Sintassi di classi e oggetti

La settimana scorsa abbiamo fatto un'[introduzione generale alla programmazione orientata agli oggetti](https://blog.federicopepe.com/2016/01/introduzione-agli-oggetti/); con questo post entreremo nello specifico analizzando la sintassi corretta da utilizzare quando si scrive una _classe_ e quando si usa un _oggetto_ in Processing.

## Sintassi della classe

Ricordo che per _classe_ intendiamo il template di partenza che utilizzeremo per creare nuovi oggetti. Per creare una nuova classe abbiamo solo bisogno di assegnargli un nome ma, se vogliamo sfruttare al massimo l'OOP, ciascuna classe avrà le seguenti caratteristiche: _nome, dati, constructor_ e _metodi_.

```java
class Car {
  // Dati
  int carLength;
  int xPos;
  int yPos;
  int speed;
  
  // Constructor
  Car() {
    carLength = 10;
    xPos = 0;
    yPos = 200;
    speed = 1;
  }
  
  // Metodi
  void display() {
    rectMode(CENTER);
    fill(0);
    rect(xPos, yPos, carLength, 10);
  }
  
  void move() {
    xPos = xPos + speed;
  }
}
```

Abbiamo scritto la nostra prima classe: **Car**. Per prima cosa sottolineo che le classi hanno sempre la prima lettera maiuscola: questo serve per differenziarle da tutti gli altri componenti che possiamo trovare in un programma (variabili, funzioni, ecc...).

Come potete vedere, la classe ha dei **dati** al suo interno che scriviamo sotto forma di variabili: la lunghezza dell'oggetto-macchina, la posizione X e Y di partenza e la velocità. Tali dati sono solo dichiarati ma non inizializzati. Per questo ci serve il **constructor** che è quella funzione speciale che serve per creare l'oggetto vero e proprio: per funzionare il constructor deve avere lo stesso nome della classe.

Nell'esempio qui sopra, ogni volta che creeremo l'oggetto _Car_ gli assegneremo di default i dati del constructor quindi una lunghezza di 10 pixel, x = 0, y = 200 e velocità pari a 1.

Infine ci sono i **metodi** ovvero le funzionalità che vogliamo dare al nostro oggetto: in questo esempio la nostra macchina sarà visualizzata sullo schermo (display) e poi si muoverà (move).

## Sintassi dell'oggetto

```java
Car myCar;

void setup() {
  size(500, 500);
  myCar = new Car();
}

void draw() {
  background(255);
  myCar.display();
  myCar.move();
}
```

Nella prima riga stiamo dichiarando una variabile globale il cui nome è **myCar** il cui data-type non sarà uno dei classici incontrati finora (integer, float, stringa, ecc...) ma sarà un oggetto _Car._

All'interno del blocco di _setup()_ inizializziamo la nostra variabile _myCar_ creando una nuova _istanza_ dell'oggetto. In pratica con la sintassi **myCar = new Car()** stiamo richiamando il _constructor_ presente all'interno della classe. Con una sola riga di codice abbiamo assegnato alla nostra _myCar_ una serie di valori: _carLength = 10, xPos = 0, yPos = 200; speed = 1_ senza doverli riscrivere.

Nel ciclo draw() richiamiamo i metodi della classe. Da notare che a differenza delle funzioni che abbiamo visto fino ad ora, dobbiamo utilizzare la cosiddetta **dot syntax** ovvero **myCar.display()** perché display è un metodo presente all'interno di myCar. Se scrivessimo solo display(); chiaramente non funzionerebbe.

## Il nostro primo programma ad oggetti

```java
Car myCar;

void setup() {
  size(500, 500);
  myCar = new Car();
}

void draw() {
  background(255);
  myCar.display();
  myCar.move();
}


class Car {
  // Dati
  int carLength;
  int xPos;
  int yPos;
  int speed;

  // Constructor
  Car() {
    carLength = 10;
    xPos = 0;
    yPos = 200;
    speed = 1;
  }

  // Metodi
  void display() {
    rectMode(CENTER);
    fill(0);
    rect(xPos, yPos, carLength, 10);
  }

  void move() {
    xPos = xPos + speed;
  }
}
```

Ecco il codice completo del nostro programma. Potete notare come la classe costituisca un nuovo blocco di codice all'interno del programma. Il codice diventa più pulito e facile da leggere perché all'interno di setup e draw troviamo pochissime righe di codice. Copiando e incollando il codice e cliccando su Run vedrete un quadratino di 10x10px che si muoverà sullo schermo.

Mi rendo conto che in alcuni punti la spiegazione possa essere arzigogolata ma spero che vi sia tutto chiaro; potete provare a cambiare alcune porzioni di codice per verificare se tutto vi torna.
