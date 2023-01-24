# Controlli condizionali III: Variabili booleane

Nel primo post dedicato ai [controlli condizionali](https://blog.federicopepe.com/2015/09/controlli-condizionali-if-else-if-else/) ho fatto un accenno alle variabili di tipo **booleano** anche se non mi sono soffermato troppo su di esse. Per il momento sappiamo solo che possono assumere un valore **true** oppure **false** ma non abbiamo ancora imparato come _dichiararle_ o _utilizzarle_.

Ovviamente dobbiamo rispettare i principi che abbiamo [già visto](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/) quando abbiamo parlato di variabili: in fase di dichiarazione dobbiamo assegnare un data type – _boolean_ in questo caso – e un nome:

`boolean var = true;`

Ecco che abbiamo creato una variabile chiamata _var_ di tipo booleano il cui suo valore iniziale sia _true._

Come possiamo utilizzare questa variabile? Ecco un esempio pratico:

```java
boolean var = true;
int ellipseX = 0;

void setup() {
  size(500, 500);
}

void draw() {
  background(0);
  ellipse(ellipseX, height/2, 50, 50);
  if(var) {
    ellipseX++;
  }
}

void mousePressed() {
  var = !var;
}
```

Questo programma è molto simile a un altro programma che [abbiamo già visto](https://blog.federicopepe.com/2015/09/variabili-in-processing-ii-operazioni-matematiche/) ma c'è una differenza sostanziale: ora, infatti, abbiamo un maggior controllo sul nostro cerchio: quando clicchiamo il mouse all'interno della finestra, il cerchio si ferma.

All'interno del ciclo _draw()_ aumentiamo il valore della variabile _ellipseX_ – che determina la posizione del cerchio – solo nel caso in cui la variabile booleana nominata _var_ sia _true._

Nella funzione mousePressed() abbiamo usato l'operatore logico NOT che inverte il valore della variabile _var_. Se infatti partiamo dal presupposto che la variabile sia _true_, come previsto dall'inizializzazione, al click del mouse _var_ diventerà **NOT _true_** quindi _false_. Viceversa, se la variabile ha un valore _false_ al click viene assegnato un valore _**NOT false**_ quindi _true_.

Mi rendo conto che questo passaggio possa essere un po' ostico quindi, per aiutarvi, riscrivo la funzione mousePressed() in modo più semplice:

```java
void mousePressed() {
 if(var) {
 var = false;
 } else {
 var = true;
 }
}
```

Con l'operatore NOT ho reso il mio codice più leggibile riducendo il numero di righe, da cinque a una soltanto, per cambiare il valore della variabile.

A questo punto vi propongo un altro esercizio: e se volessi fare in modo che il mio cerchio anziché fermarsi torni indietro al click del mouse? Buon lavoro!
