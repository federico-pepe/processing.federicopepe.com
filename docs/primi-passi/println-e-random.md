# Le funzioni println() e random()

## println()

La [settimana scorsa](https://blog.federicopepe.com/2015/09/variabili-in-processing-ii-operazioni-matematiche/) ho accennato alla funzione println(); per mostrarne bene il funzionamento, ho realizzato questo breve video:

![type:video](/assets/video/Processing_println.mp4)

Il codice di questo sketch è molto semplice:

```java
void setup() {
  size(700, 500);
}
void draw() {
  println("Mouse X: " + mouseX + " : Mouse Y: " + mouseY);
}
```

Ho creato una finestra di 700x500 pixel e, senza che venga disegnato nulla, chiedo al programma di mostrarmi nella console di debug il valore di mouseX e di mouseY in ogni istante. Anche se in questo caso le variabili sono soltanto due, per aiutarmi a capire di quale stiamo parlando ho aggiunto un breve testo esplicativo. Come si evince dal codice, questo testo aggiuntivo è inserito tra virgolette " " e utilizzo il simbolo + per concatenare le varie parti della frase.

Per completezza è giusto dire che esistono anche le funzioni **print()** e **printArray().** Quest'ultima ci sarà molto utile quando cominceremo a utilizzare gli array, mentre, per quanto riguarda la prima, l'unica differenza rispetto a **println()** è che il testo non va automaticamente a capo alla fine della frase.

## random()

Possiamo utilizzare la funzione **random()** per generare un po' di caos e rendere i nostri sketch interessanti affidandoci alla casualità. Questa funzione può accettare uno o due valori _float_ in input e restituisce sempre un valore di tipo _float_. Se usiamo un parametro, la funzione restituirà un valore causale compreso tra 0 e il parametro che abbiamo inserito; se, invece, inseriamo due parametri, il valore in output sarà compreso tra essi.

Come dicevo, questa funzione è utile per creare dei programmi semplici ma di impatto.

```java
/*
 * Utilizzo della funzione random() - Esempio: 1
 * by Federico Pepe
 * http://blog.federicopepe.com
 */

void setup() {
  size(700, 500);
  background(255);
}
void draw() {
  ellipse(random(width), random(height), 10, 10 );
}
```

Questo sketch crea dei cerchi di dimensioni 10, 10 in posizioni casuali all'interno della finestra: la x è compresa tra 0 e la larghezza della finestra e la y tra 0 e l'altezza.

![random - esempio 1](/assets/images/processing_random_esempio_1-1024x800.png)

### Problema:

Se volessimo fare in modo che i cerchi abbiano tutti dimensioni diverse comprese tra 10 e 50? Immagino che qualcuno di voi abbia pensato a qualcosa del genere:

ellipse(random(width), random(height), random(10, 50),  random(10,50));

Purtroppo questa soluzione non è corretta: quante possibilità abbiamo che il numero casuale estratto sia per la larghezza che per l'altezza del cerchio sia uguale disegnando, dunque, un cerchio? Se inserite questa riga di codice nell'esempio qui sopra, noterete che verranno disegnati principalmente ellissi.

Dobbiamo, quindi, fare in modo che la dimensione sia casuale e compresa tra 10 e 50 ma che sia uguale per larghezza e altezza. Vi viene qualche idea?

Forse una variabile potrebbe tornarci utile!

Creiamo una variabile di nome _radius_ di tipo _float_ e in ogni ciclo draw() gli assegnamo un valore compreso tra 0 e 50 con la funzione random. Utilizziamo, poi, la variabile all'interno della funzione ellipse sia per la larghezza che per l'altezza.

```java
/*
 * Utilizzo della funzione random() - Esempio: 2
 * by Federico Pepe
 * http://blog.federicopepe.com
 */
float radius;

void setup() {
  size(700, 500);
  background(255);
}
void draw() {
  radius = random(10, 50);
  ellipse(random(width), random(height), radius, radius);
}
```

![Random esempio 2](/assets/images/processing_random_esempio_2-1024x800.png)]

Come ultimo esempio, modifichiamo ulteriormente il nostro programma per aggiungere un po' di colore. Anche in questo caso, utilizziamo la funzione random limitandola in un range compreso tra 0 e 255 ([vi ricordate la lezione sui colori RGB, vero?](/primi-passi/colori-rgb)).

Aggiungiamo nel nostro programma:

`fill(random(255), random(255), random(255));`

![Processing random - esempio 3](/assets/images/processing_random_esempio_3-1024x800.png)

Voilà!
