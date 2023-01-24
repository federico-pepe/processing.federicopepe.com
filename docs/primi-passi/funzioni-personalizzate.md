# Funzioni Personalizzate

Iniziamo con un nuovo importante capitolo nel nostro percorso di introduzione alla programmazione con Processing. Se state seguendo questa serie di post dall'inizio, arrivati a questo punto vi sarete resi conto che negli esempi che ho proposto ho sempre cercato di seguire due regole auree della programmazione:

1. scrivere il minor numero di righe di codice possibile
2. scrivere codice semplice da leggere e interpretare.

Per quanto riguarda il primo punto, non penso che i programmatori siano pigri ma, al contrario, mi piace pensare che amino arrivare dritti al punto, senza perdersi in fronzoli o distrazioni.

In merito alla leggibilità, capirete quanto è importante scrivere bene il proprio codice quando vi capiterà di dover rimettere mano a dei progetti realizzati qualche mese o, addirittura, qualche anno prima.

Come anticipavo nell'incipit, con questo post cominceremo  un percorso che ci porterà a capire e a utilizzare la _**programmazione orientata agli oggetti (OOP)**_, uno dei paradigmi fondamentali della programmazione moderna.

## Un mondo di funzioni

Fin dal primo post abbiamo parlato di **funzioni** e, con il susseguirsi degli articoli, ne abbiamo utilizzate parecchie. Abbiamo imparato che queste funzioni ci permettono, ad esempio, di [impostare la grandezza della finestra](https://blog.federicopepe.com/2015/07/schermo-pixel-e-linee/) di lavoro oppure di [disegnare forme geometriche](https://blog.federicopepe.com/2015/07/primitive-2d-point-line-rect-ellipse-triangle/).

Alcune di esse hanno bisogno di uno o più parametri per funzionare correttamente, penso, ad esempio, a _fill()_ altre, invece, devono semplicemente essere richiamate e non necessitano di ulteriori dati come _setup()_ o _draw()_.

I creatori di Processing hanno già inserito all'interno del linguaggio una serie di funzioni per rendere il linguaggio semplice da utilizzare. Provate a pensare a quanto sarebbe difficile disegnare un cerchio senza avere a disposizione la funzione _ellipse()_.

Come per le variabili built-in, le parole che identificano le funzioni già inserite all'interno di Processing sono riconoscibili perché vengono evidenziate automaticamente. Ovviamente è possibile creare delle funzioni personalizzate a patto che il nome scelto non sia già riservato da una funzione built-in.

## Modularità e riusabilità

Il numero di righe di codice di un programma determina la sua complessità; cominciare a utilizzare funzioni personalizzate e, come vedremo tra qualche settimana, gli oggetti ci permette di rendere il codice modulare e riusabile.

Perché questo punto è molto importante? Un programma modulare è facile da debuggare e da modificare e/o riadattare alle proprie esigenze. Vi ricordate la differenza tra un [programma con parametri hard-coded e lo stesso programma scritto con le variabili](https://blog.federicopepe.com/2015/08/variabili-built-in/)?

Il principio è lo stesso ed è come dividere il contenuto di un manuale in capitoli: grazie alla modularità delle funzioni possiamo trovare subito le porzioni di codice che ci interessa leggere o modificare.

In merito alla riusabilità: se scriviamo delle funzioni complesse, possiamo tranquillamente copiarle e incollarle in un nuovo progetto senza perdere tempo a riscriverle da capo con un notevole risparmio di tempo e risorse.

## Return e void

Arriviamo al punto: come si scrive una funzione? Innanzitutto dobbiamo capire se la nostra funzione è pensata per **restituire** un valore oppure no. Facciamo un esempio per ciascun caso:

1. Una funzione che, ogni volta che viene richiamata, mi disegni un fiore sullo schermo.
2. Una funzione matematica che aggiunga 5 a ogni numero che viene utilizzato come parametro.

Nel primo caso la funzione non restituisce alcun valore: disegna semplicemente un fiore sullo schermo. In questa funzione potremmo comunque passare dei parametri come, ad esempio, la posizione iniziale del fiore ma non ci verrà restituito nessun valore né numerico né di testo dalla funzione stessa.

Nel secondo caso, invece, utilizziamo una funzione proprio per ricevere in cambio un numero.

Le due parole magiche che dovrò utilizzare in Processing sono **void** e **return**.

## La nostra prima funzione: Flower

```java
void setup() {
  size(700, 700);
  background(255);  
}

void draw() {
  flower(width/2, height/2);
}

void flower(int posizioneX, int posizioneY) {
  noStroke();
  fill(0, 255, 0);
  rectMode(CENTER);
  rect(posizioneX, posizioneY+100, 25, 100);
  fill(255, 0, 255);
  ellipse(posizioneX-50, posizioneY, 70, 70);
  ellipse(posizioneX, posizioneY-50, 70, 70);
  ellipse(posizioneX+50, posizioneY, 70, 70);
  ellipse(posizioneX, posizioneY+50, 70, 70);
  fill(255, 255, 0);
  ellipse(posizioneX, posizioneY, 50, 50);
  noFill();
}
```

Ecco il risultato:[![Funzioni personalizzate: flower](/assets/images/Processing_funzioni_personalizzate-997x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_funzioni_personalizzate.png)

La parte di codice che ci interessa parte dalla linea 10:

void flower(int posizioneX, int posizioneY) {

Sto dicendo a Processing di creare una funzione che non restituirà nessun parametro (_void_) di nome _flower_ che accetta due parametri in input di tipo integer: _posizioneX_ e _posizioneY_. La parentesi graffa alla fine mi serve per aprire il blocco di codice della funzione.

Nelle linee successive disegno il fiore utilizzando più volte la funzione _ellipse_ per i petali e il pistillo e un _rect_ per il gambo. I parametri _posizioneX_ e _posizioneY_ vengono richiamati per impostare correttamente la posizione del fiore nella finestra.

Con la parentesi graffa finale, chiudo il blocco di codice della funzione.

Una volta scritta la funzione, è sufficiente richiamarla in _setup()_ o in _draw()_ passandogli le due variabili di tipo integer che la funzione si aspetta di ricevere.

Ora se io volessi disegnare più fiori all'interno della finestra, sarebbe sufficiente richiamare la funzione flower il numero di volte necessario:

```java
void setup() {
  size(700, 700);
  background(255);  
}

void draw() {
  flower(width/2, height/2);
  flower(100, 200);
  flower(500, 300);
  flower(100, 600);
}

void flower(int posizioneX, int posizioneY) {
  noStroke();
  fill(0, 255, 0);
  rectMode(CENTER);
  rect(posizioneX, posizioneY+100, 25, 100);
  fill(255, 0, 255);
  ellipse(posizioneX-50, posizioneY, 70, 70);
  ellipse(posizioneX, posizioneY-50, 70, 70);
  ellipse(posizioneX+50, posizioneY, 70, 70);
  ellipse(posizioneX, posizioneY+50, 70, 70);
  fill(255, 255, 0);
  ellipse(posizioneX, posizioneY, 50, 50);
  noFill();
}
```

[![Funzioni personalizzate in Processing](/assets/images/Processing_funzioni_personalizzate_2-997x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_funzioni_personalizzate_2.png)

Se volessi creare un prato pieno di fiori, potrei inserire la funzione all'[interno di un ciclo](https://blog.federicopepe.com/2015/11/loop-for-e-nesting/) e, ovviamente, potrei aggiungere dei parametri ulteriori per creare, ad esempio, fiori di colore e grandezza diversi:

```java
void setup() {
  size(700, 700);
  background(255);
  for(int i = 0; i < 20; i++) {
    flower(int(random(width)), int(random(height)), color(random(255), random(255), random(255)), int(random(60, 100)));
  }
}

void draw() {
  
}

void flower(int posizioneX, int posizioneY, color colore, int petali) {
  noStroke();
  fill(0, 255, 0);
  rectMode(CENTER);
  rect(posizioneX, posizioneY+100, 25, 100);
  fill(colore);
  ellipse(posizioneX-50, posizioneY, petali, petali);
  ellipse(posizioneX, posizioneY-50, petali, petali);
  ellipse(posizioneX+50, posizioneY, petali, petali);
  ellipse(posizioneX, posizioneY+50, petali, petali);
  fill(255, 255, 0);
  ellipse(posizioneX, posizioneY, 50, 50);
  noFill();
}
```

[![Un campo di fiori](/assets/images/Processing_funzioni_personalizzate_3-997x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_funzioni_personalizzate_3.png)

## Funzioni che restituiscono valori

Passiamo ora al secondo esempio:

```java
void setup() {
  println(aggiungiCinque(10));
}

void draw() {
}

int aggiungiCinque(int numero) {
  return numero+5;
}
```

Abbiamo creato una funzione che restituisce un tipo di dato _integer_ chiamata _aggiungiCinque_ che accetta un parametro di tipo _integer_. Con la parola chiave **return** restituiamo il valore passato come parametro a cui abbiamo sommato 5;

Nella funzione _setup()_ abbiamo chiamato la nostra funzione _aggiungiCinque(10)_ passando il valore 10. Nella console, ci verrà stampato, correttamente, il valore 15.

È di fondamentale importanza indicare correttamente sia il tipo di valore che la funzione restituirà in output sia quello che può accettare in input. Se, infatti, passassimo il valore 10.5, un float, Processing ci restituirebbe un errore come nell'immagine:

[![Errore in input](/assets/images/Processing_the_method_is_not_applicable_for_the_argument-1024x951.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_the_method_is_not_applicable_for_the_argument.png)

Modificando la funzione per accettare un float ma lasciando la restituzione di un parametro integer otteniamo un altro tipo di errore sul return:

[![Errore sull'output](/assets/images/Processing_cannot_convert-1024x951.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_cannot_convert.png)
