# Variabili built-in

Nell'[ultimo post](https://blog.federicopepe.com/2015/08/blocchi-di-codice-e-flusso-setup-e-draw/), abbiamo creato il nostro primo programma interattivo sfruttando le potenzialità della funzione _draw()_ che, vi ricordo, viene eseguita in un loop costante a 60fps (di default) dal momento in cui avviamo il nostro programma fino a quando non lo fermiamo.

Negli ultimi due esempi di codice che ho postato ho aggiunto, senza dare troppe spiegazioni, due parole **mouseX** e **mouseY** che possiamo definire come _variabili built-in_.

È arrivato il momento di capire cosa intentiamo per _variabili_, come funzionano e se ce ne sono altre che possiamo utilizzare.

## **Hard coding vs variabili**

In tutti i programmi che abbiamo realizzato finora, abbiamo sempre scritto i parametri che volevamo utilizzare direttamente nelle funzioni. Per fare un esempio: per disegnare un cerchio con un diametro di 100 pixel al centro di una finestra di dimensione 500x500 pixel, la linea di codice che abbiamo usato è:

`ellipse(250, 250, 100, 100);`

Questa pratica viene definita **hard coding** ed è fortemente sconsigliata perché rende i nostri programmi lunghi da modificare e inutilizzabili o imprecisi al variare di alcune condizioni (se, riprendendo l'esempio di cui sopra, modifico la dimensione della finestra portandola a 700x700 pixel, il cerchio non sarà più centrato come prima).

Più avanti, in questo post, riprenderò l'esempio qui descritto con codice e screenshot.

Per ovviare a questo problema si utilizzano delle **variabili** ovvero dei parametri che possono assumere un valore che può essere cambiato durante l'esecuzione del programma attraverso, ad esempio, semplici funzioni matematiche.

## Variabili built-in

È possibile creare un numero di variabili a nostro piacimento e con tipologie di dati differenti e, in un altro post, vi spiegherò come fare. In questo articolo voglio concentrarmi su un insieme particolare di variabili: quelle cosiddette _built-in_ ovvero già presenti "all'interno" di Processing.

Una cosa molto importante quando si utilizzano variabili è prestare attenzione alla sintassi corretta: Processing ci viene in aiuto colorandole di rosa.

![Built-in variables](/assets/images/Processing-variabili-built-in-880x1024.png)

### mouseX, mouseY

Abbiamo già usato _mouseX_ e _mouseY_ in uno sketch e abbiamo capito che, se inseriamo queste variabili, all'interno del blocco di codice _draw()_ ci restituiscono in tempo reale i valori X e Y del mouse quando ci muoviamo all'interno della finestra.

### width, height

_width_ e _height_ significano letteralmente larghezza e altezza e, com'è facile intuire, restituiscono le dimensioni della finestra dopo che queste sono state impostate nel blocco di codice _setup()_.

Analizziamo insieme questo codice e il risultato finale:

```java
/*
 * Hard coding vs built-in variables
 * by Federico Pepe
 * http://blog.federicopepe.com
 */
void setup() {
  // Imposto la grandezza della finestra a 500x500px
  size(500, 500);
  // Imposto colore di riempimento ed elimino il bordo
  noStroke();
  fill(255, 0, 0, 100);
  // Disegno un cerchio di diametro 100px al centro
  // della finestra utilizzando l'hard-coding
  ellipse(250, 250, 100, 100);
  // Disegno un cerchio di diametro 150px al centro
  // della finestra utilizzando due variabili built-in
  ellipse(width/2, height/2, 150, 150);
}
```

![Processing hard coding vs built-in variables](/assets/images/Processibng-hardcoding_vs_builtinvariables-988x1024.png)

Abbiamo disegnato due cerchi di diametro differente in una finestra di 500x500px. Nel primo caso i parametri x e y sono stati inseriti direttamente (hard-coding) quindi:

`ellipse(250, 250, 100, 100);`

Nel secondo cerchio, invece, abbiamo utilizzato le variabili width e height e, per centrare il cerchio, le abbiamo divise per 2.

`ellipse(width/2, height/2, 150, 150);`

Cosa accade se modifico la dimensione della finestra?

```java
/*
 * Hard coding vs built-in variables
 * by Federico Pepe
 * http://blog.federicopepe.com
 */
void setup() {
  // Imposto la grandezza della finestra a 700x700px
  size(700, 700);
  // Imposto colore di riempimento ed elimino il bordo
  noStroke();
  fill(255, 0, 0, 100);
  // Disegno un cerchio di diametro 100px al centro
  // della finestra utilizzando l'hard-coding
  ellipse(250, 250, 100, 100);
  // Disegno un cerchio di diametro 150px al centro
  // della finestra utilizzando due variabili built-in
  ellipse(width/2, height/2, 150, 150);
}
```

![Hard coding vs Variabili 2](/assets/images/Processing-hardcoding-vs-variabili-2-997x1024.png)

Come previsto, il primo cerchio si trova spostato in alto a sinistra rispetto al centro della finestra mentre, il secondo, è rimasto perfettamente centrato. Per ottenere a livello visivo lo stesso effetto di prima nel caso del primo cerchio dovrei andare a modificare direttamente i parametri (oppure sostituirli con delle variabili).

### pmouseX, pmouseY

Le ultime due variabili built-in di cui voglio parlarvi sono _pmouseX_ e _pmouseY_ che, a differenza di mouseX e mouseY restituiscono i valori x e y del mouse del frame _precedente_ a quello corrente.

Come possiamo utilizzarle in modo creativo? Con poche righe di codice possiamo, ad esempio, creare un programma per disegnare:

```java
/*
 * Drawing Tool
 * by Federico Pepe
 * http://blog.federicopepe.com
 */
void setup() {
  size(700, 700);
  background(0);
}

void draw() {
  stroke(255);
  line(pmouseX, pmouseY, mouseX, mouseY);
}
```

![Processing example](/assets/images/Processing-Drawing-Tool-997x1024.png)
