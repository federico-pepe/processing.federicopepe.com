# "OOP: Classi e oggetti, parte 2"

Ripartiamo da dove ci siamo fermati con l'[ultimo post](https://blog.federicopepe.com/2016/01/oop-sintassi-di-classi-e-oggetti/): abbiamo scritto la nostra prima classe e abbiamo creato il nostro primo oggetto. Nell'approfondimento di oggi su classi e oggetti parleremo di alcune questioni importanti: come mantenere pulito il codice quando si lavora con le classi, come passare parametri al constructor e, infine, come creare _n_ oggetti.

## Operazione pulizia: utilizzare le Tab

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

Il nostro codice ora è lungo 40 righe in tutto e la classe _Car_ occupa la maggior parte dello spazio. Immaginate per un secondo di avere tra le mani un programma molto complesso, che utilizza tante tipologie di oggetti differenti. Sarebbe davvero problematico andare a cercare di volta in volta scorrendo in su e in giù la porzione di codice che si riferisce all'oggetto che vogliamo utilizzare.

Per fortuna Processing viene in nostro aiuto con una funzione molto comoda: le Tab.

![Crea una nuova Tab su Processing](/assets/images/OOP_Processing_New_Tab-1024x898.png)

Cliccando sulla freccia che punta in basso accanto al nome del nostro sketch, si aprirà un menu con diverse opzioni. Clicchiamo su _New Tab_ (su Mac la scorciatoia è **⇧⌘N**). A questo punto il programma ci chiederà il nome che vogliamo dare alla nostra tab; dovendo spostare lì la classe _Car_, utilizziamo lo stesso nome sempre con l'iniziale maiuscola.

Una volta cliccato su _OK_, l'editor creerà un altro file _.pde_ che verrà aggiunto automaticamente alla cartella dove abbiamo salvato il nostro sketch (la scorciatoia per vedere velocemente la cartella è **⌘K**).

![Sketch Folder](/assets/images/Processing_Sketch_Folder-1024x636.png)

A questo punto facciamo copia-incolla del codice della classe nella nuova tab e proviamo a cliccare _Run._ Il programma dovrebbe aprirsi e funzionare esattamente come prima con la differenza che, ora, il codice del file principale – quello nominato sketch\_160115a.pde in questo esempio – è molto più breve e pulito.

## Passare parametri al constructor

La nostra classe _Car_ è ora funzionale e pulita ma è ancora migliorabile: ho scritto [più volte](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/) dell'importanza di utilizzare le variabili invece di parametri hard-coded ma il constructor che abbiamo ora genererà sempre oggetti con le stesse caratteristiche: la lunghezza sarà sempre pari a 10 pixel, la posizione di partenza sarà x = 0 e y = 200 e la velocità pari a 1.

La buona notizia è che possiamo inserire nella nostra classe più constructor mantenendo una sintassi simile a quella che già conosciamo; dobbiamo solo aggiungere, all'interno della parentesi tonda, le variabili che decidiamo di passare ai nostri oggetti.

In questo primo esempio, aggiungiamo la possibilità di modificare la lunghezza della nostra macchina.

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
  
  // Secondo Constructor
  Car(int tempCarLength) {
    carLength = tempCarLength;
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

In questa nuova versione ho aggiunto alla classe un nuovo constructor che accetta un solo parametro di tipo integer. Quando il parametro viene passato devo utilizzare una variabile temporanea, motivo per cui ho inserito la variabile **tempCarLength**. La variabile temporanea dovrà poi essere assegnata alla variabile relativa all'interno del costructor: _carLength = tempCarLength._

Questo è il momento in cui è necessario diventare molto ordinati e scrupolosi con i nomi che diamo alle nostre variabili, il rischio è di complicarci inutilmente la vita.

Ora che abbiamo un nuovo constructor, torniamo al nostro sketch principale e modifichiamo l'inizializzazione da così:

myCar = new Car();

a così:

myCar = new Car(25);

Proviamo a lanciare il nostro sketch.

![Variabili al constructor](/assets/images/Processing_passing_variables_to_constructor-988x1024.png)

Il nostro rettangolo sarà ora lungo 25 pixel.

Cosa succede se proviamo a passare al nostro constructor una variabile di tipo _float_?

myCar = new Car(25.7);

Ovviamente ci verrà restituito un errore: _The constructor "Car(float)" does not exist._

## Constructor, constructor, constructor

Il prossimo passaggio sarà creare tanti constructor quanti sono i dati che il nostro oggetto contiene: nel nostro programma vorremmo, ad esempio, decidere anche la posizione x e y di partenza oltre, ovviamente, diversi valori di velocità. Possiamo fare anche un passaggio in più: aggiungiamo una nuova variabile che contenga anche il colore della macchina.

Vi invito a provare a modificare la classe per conto vostro e di non guardare subito il codice qui sotto. In questo modo capirete se, effettivamente, vi è tutto chiaro.

```java
class Car {
  // Dati
  int carLength;
  float xPos;
  int yPos;
  float speed;
  color c;

  // Constructor
  Car() {
    carLength = 10;
    xPos = 0;
    yPos = 200;
    speed = 1;
    c = color(0);
  }
  
  // Secondo Constructor
  Car(int tempCarLength) {
    carLength = tempCarLength;
    xPos = 0;
    yPos = 200;
    speed = 1;
    c = color(0);
  }
  
  // Secondo Constructor
  Car(int tempCarLength, int tempXPos) {
    carLength = tempCarLength;
    xPos = tempXPos;
    yPos = 200;
    speed = 1;
    c = color(0);
  }
  
  Car(int tempCarLength, int tempXPos, int tempYPos) {
    carLength = tempCarLength;
    xPos = tempXPos;
    yPos = tempYPos;
    speed = 1;
    c = color(0);
  }
  
  Car(int tempCarLength, int tempXPos, int tempYPos, float tempSpeed) {
    carLength = tempCarLength;
    xPos = tempXPos;
    yPos = tempYPos;
    speed = tempSpeed;
    c = color(0);
  }
  
  Car(int tempCarLength, int tempXPos, int tempYPos, float tempSpeed, color tempColor) {
    carLength = tempCarLength;
    xPos = tempXPos;
    yPos = tempYPos;
    speed = tempSpeed;
    c = tempColor;
  }

  // Metodi
  void display() {
    rectMode(CENTER);
    fill(c);
    rect(xPos, yPos, carLength, 10);
  }

  void move() {
    xPos = xPos + speed;
  }
}
```

Sottolineo un paio di cose:

1. Ho aggiornato la nostra classe senza toccare il codice del nostro sketch principale. Questa è la potenza della programmazione orientata agli oggetti: modificare porzioni di codice senza andare a intaccare le altre parti che compongono il programma.
2. Ho utilizzato per la prima volta il _datatype_ color. Non è niente di difficile ma, dal momento che non ho intenzione di spiegare come funziona in questo post, vi invito a [leggere il manuale](https://processing.org/reference/color_datatype.html).
3. Ho cambiato il datatype di speed in _float_ e sono stato costretto a cambiarlo anche per _xPos_ dal momento che nella funzione move() i due parametri vengono sommati. Se avessi lasciato xPos come int, Processing mi avrebbe restituito un errore.

Ora che la nostra classe è completa, possiamo sbizzarrirci a passare quanti parametri vogliamo, l'importante è  ricordarsi l'ordine dei parametri e i tipi di dati accettati:

myCar = new Car(25, 50, 200, 0.5, color(255, 255, 0));

Il bello è che possiamo utilizzare anche delle funzioni per passare i parametri. Vi ricordate di [random](https://blog.federicopepe.com/2015/09/println-e-random/)?

myCar = new Car(25, 50, 200, random(5), color(random(255), random(255), random(255)));

## Creiamo _n_ oggetti

Nell'introduzione agli oggetti avevo specificato che un punto di forza dell'OOP è poter creare più istanze dello stesso oggetto. Come possiamo, dunque, creare 3 macchine?

Riprendiamo in mano il nostro sketch principale e aggiungiamo altre due variabili di tipo _Car_ chiamate myCar2 e myCar3, in setup() creiamo due nuove istanze degli oggetti e, in draw() ci assicuriamo di richiamare, per ciascuna, i metodi display() e move().

```java
Car myCar, myCar2, myCar3;

void setup() {
  size(500, 500);
  myCar = new Car(25, 50, 200, random(5), color(random(255), random(255), random(255)));
  myCar2 = new Car(int(random(5, 50)), int(random(width)), int(random(height)), random(5), color(random(255), random(255), random(255)));
  myCar3 = new Car(int(random(5, 50)), int(random(width)), int(random(height)), random(5), color(random(255), random(255), random(255)));
}

void draw() {
  background(255);
  myCar.display();
  myCar.move();
  
  myCar2.display();
  myCar2.move();
  
  myCar3.display();
  myCar3.move();
}
```

Premiamo su _Run_:

![Abbiamo creato 3 oggetti Car](/assets/images/Creare_n_oggetti-988x1024.png)

Fino a qui tutto bene, ma, a questo punto la domanda che sorge spontanea è: se volessimo creare _decine_ o _centinaia_ di oggetti? Dovremmo impazzire con il copia-incolla. Chiaramente esiste una soluzione più comoda: utilizzare gli _array_ che, per l'appunto, saranno il prossimo argomento che tratteremo.

## Compiti a casa

È arrivato il momento di dimostrare di aver capito come funziona la programmazione ad oggetti: riprendete in mano l'esercizio Bouncing Ball ([parte 1](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-1/) e [parte 2](https://blog.federicopepe.com/2015/12/esercizio-bouncing-ball-parte-2/)) e modificate il codice per renderlo object-oriented.
