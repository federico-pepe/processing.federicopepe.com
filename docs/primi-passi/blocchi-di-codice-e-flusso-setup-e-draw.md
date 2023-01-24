# Blocchi di codice e flusso: setup() e draw()

Oggi introduciamo due concetti di base molto importanti che ci porteranno a realizzare dei programmi _interattivi_ con Processing.

Fino ad oggi, ci siamo limitati a scrivere una linea di codice dopo l'altra e abbiamo imparato che quando clicchiamo sul pulsante **Run**, se non ci sono errori, ciascuna di esse viene processata in ordine dalla prima all'ultima.

Gli sketch che abbiamo realizzato nelle scorse lezioni sono belli ma poco interessanti perché siamo abituati a utilizzare programmi che, una volta lanciati, cambiano aspetto in base al procedere del tempo e a come interagiamo con essi attraverso mouse, tastiera, ecc...

Pensate, ad esempio, allo screensaver del vostro computer oppure a un qualsiasi gioco per pc: tutte queste applicazioni partono da uno stato iniziale in cui vengono _settate_ alcune impostazioni e, mentre il programma funziona, il computer controlla costantemente la posizione del mouse oppure se abbiamo premuto un determinato tasto. Idealmente questo controllo dovrebbe avvenire 30 volte al secondo.

## Le funzioni setup() e draw()

In Processing esistono due funzioni molto importanti: **setup()** e **draw()**. Prima di procedere con la spiegazione del loro funzionamento, dobbiamo capire come dividere in porzioni o, per meglio dire, _blocchi_ il nostro codice in modo da suddividere in modo preciso le operazioni che saranno eseguite in fase iniziale di setup e quelle che, invece, saranno costantemente ripetute dal computer in draw.

Per delimitare l'inizio e la fine dei blocchi di codice si usano le parentesi graffe:

```java
void setup() {
  // Blocco di codice di setup
}

void draw() {
  // Blocco di codice di draw
}
```

Vi chiedo di ignorare, per il momento, il significato di _void_ e il fatto che, a differenza delle funzioni usate finora, non abbiamo inserito nessun parametro all'interno delle parentesi tonde; torneremo su questo argomento più avanti quando tratteremo in modo più approfondito le funzioni.

Ora possiamo riprendere alcuni esempi delle lezioni precedenti e ragionare su quali porzioni di codice siano da inserire in _setup()_ e quali in _draw()_. Sottolineo ancora una volta che le linee inserite nel blocco di codice setup verranno eseguite **una sola volta** all'avvio del programma mentre, quelle nel blocco draw, saranno **processate continuamente** dal nostro computer a una velocità, di default in Processing, di _60 frame per_ secondo, d'ora in poi abbreviato in _fps_.

Impostare la dimensione della finestra è un'operazione che può e deve essere eseguita una volta sola; disegnare un cerchio in una determinata posizione e impostare il suo colore è un'operazione che, invece, può essere ripetuta.

Ecco dunque che questo codice, preso dalla [scorsa lezione](https://blog.federicopepe.com/2015/08/colori-rgb/):

```java
size(500, 500);
fill(255, 0, 0);
ellipse(250, 250, 150, 150);
```

diventa:

```java
void setup() {
  // Questo codice verrà eseguito una sola volta
  size(500, 500);
}

void draw() {
  // Questo codice verrà ripetuto a una frequenza di 60fps
  fill(255, 0, 0);
  ellipse(250, 250, 150, 150);
}
```

Se copiate e incollate questi due esempi in Processing e cliccate su Run non noterete alcuna differenza a livello visivo ma il computer sta processando questi programmi in modo diverso:

Nel primo caso:

```
- Imposta la dimensione della finestra a 500x500px
- Imposta il colore di riempimento: RGB(255, 0, 0)
- Disegna un ellisse con centro x = 250, y = 250, largh. = 150 e alt. = 150
```

Nel secondo caso:

```
- Imposta la dimensione della finestra a 500x500px
- Imposta il colore di riempimento: RGB(255, 0, 0)
- Disegna un ellisse con centro x = 250, y = 250, largh. = 150 e alt. = 150
- Imposta il colore di riempimento: RGB(255, 0, 0)
- Disegna un ellisse con centro x = 250, y = 250, largh. = 150 e alt. = 150
- Imposta il colore di riempimento: RGB(255, 0, 0)
- Disegna un ellisse con centro x = 250, y = 250, largh. = 150 e alt. = 150
- Imposta il colore di riempimento: RGB(255, 0, 0)
- Disegna un ellisse con centro x = 250, y = 250, largh. = 150 e alt. = 150
...
```

Le ultime righe di informazioni sono ripetute 60 volte al secondo all'infinito finché non interrompiamo il programma premendo il tasto **Stop**_._

## La nostra prima animazione

Dal momento che con questo esempio non riusciamo a vedere nulla di diverso sullo schermo, rendiamo le cose un po' più interessanti introducendo un'altra novità di cui parleremo in modo approfondito nelle prossime lezioni: anziché impostare una posizione x e y predefinita, disegniamo il nostro cerchio rosso in base alla posizione del mouse (_mouseX_ e _mouseY_):

```java
void setup() {
  size(500, 500);
}

void draw() {
  background(0);
  fill(255, 0, 0);
  ellipse(mouseX, mouseY, 150, 150);
}
```

Ecco cosa accade:

![Processing Animation](/assets/img/Processing_Animation.gif)

Anche se in questa immagine non si vede il cursore del mouse, il nostro occhio percepirà il movimento del cerchio come un'animazione: abbiamo creato il nostro primo sketch interattivo perché risponde a un input esterno e che cambia col passare del tempo.

A questo punto, per essere sicuri di aver compreso la differenza tra setup e draw possiamo domandarci: cosa accade se spostiamo _background(0)_ dal blocco draw a quello di setup?

```java
void setup() {
  size(500, 500);
  background(0);
}

void draw() {
  fill(255, 0, 0);
  ellipse(mouseX, mouseY, 150, 150);
}
```

Questa volta il colore di sfondo viene impostato solo una volta all'avvio del programma, questo significa che ogni volta che verrà mosso il mouse, un nuovo cerchio verrà disegnato sopra ai precedenti.

![Processing setup and draw](/assets/img/Processing_setup_draw-988x1024.png)