# Loop II: for e nesting

Come accennato nel [post precedente](https://blog.federicopepe.com/2015/11/loop-while/), esistono due tipologie di loop: quelli con [while](https://blog.federicopepe.com/2015/11/loop-while/) e quelli con for. Oggi ci concentreremo su questi ultimi che, come dicevo, sono quelli che preferisco utilizzare.

Ripassiamo velocemente come funziona il ciclo while: questa tipologia di loop esegue un blocco di codice finché la condizione prevista tra parentesi è _true_.
```
while(condizione) {
 // Blocco di codice
}
```
Il motivo per cui io non amo utilizzare il while nasce dal fatto che la variabile deve essere dichiarata e inizializzata all'esterno del loop, verificata nella condizione e incrementata all'interno del loop.

La stessa variabile viene quindi utilizzata in punti diversi del codice e questo, nel caso di programmi piuttosto complessi, può creare non poca confusione.

## For

Per ovviare al problema sopra descritto, ci affidiamo ai cicli for dove l'inizializzazione, la verifica e l'incremento della variabile "contatore" avviene all'interno della condizione.

Riprendiamo l'esempio del post precedente e riscriviamolo utilizzando il for:

```java
void setup() {
  size(700, 500);
  background(255);
  for(int y = 10; y < height; y+=10) {
    line(100, y, 600, y);
  }
}

void draw() {
}
```

Il codice ora risulta più pulito e più facile da leggere: in una sola riga abbiamo iniziato il ciclo, dichiarato e inizializzato la variabile contatore _int y = 10;_ posto la condizione _y < height;_ e, infine, incrementato la variabile di 10 a ogni ciclo: _y += 10_. È importante sottolineare che questi tre blocchi devono essere separati dal punto e virgola, come mostrato nell'esempio.

## Loop in draw()

Prendiamo in considerazione la possibilità di inserire un ciclo all'interno della funzione _draw()_ che, come abbiamo avuto modo di ripetere fino alla nausea, è essa stessa una funzione che si ripete costantemente.

```java
void setup() {
  size(700, 500);
  background(255);
}

void draw() {
  for(int y = 10; y < height; y+=10) {
    line(100, y, 600, y);
  }
}
```

Il funzionamento di questo programma è più semplice di quello che si può pensare: nel primo ciclo di _draw()_ il programma processerà per intero il loop _for_ (quindi la variabile y partirà da un valore 10 e poi verrà aumentata di 10 fino al raggiungimento del valore 690). Quando la condizione diventa _false_ e il loop _for_ si conclude, il ciclo _draw()_ aggiorna lo schermo visualizzando tutte le linee e poi riparte per il secondo ciclo. A quel punto y verrà reimpostata al suo valore iniziale 10 e ripeterà nuovamente l'interno processo. Alla velocità di 60fps, non si riesce a vedere nessun tipo di animazione; per farlo, è sufficiente aggiungere una variabile random:

```java
void setup() {
  size(700, 500);
  background(255);
}

void draw() {
  for(int y = 10; y < height; y+=10) {
    stroke(random(255), 0, random(255));
    line(100, y, 600, y);
  }
}
```

## Loop nesting

La parola inglese nesting significa _annidamento_; quando usato in programmazione e, in particolare, in questo contesto, intendiamo la possibilità di inserire un loop for all'interno di un altro loop. Se, ad esempio, volessimo disegnare una griglia di rettangoli a coprire l'intera larghezza e altezza della nostra finestra potremmo procedere così:

```java
void setup() {
  size(700, 500);
  background(255);
}

void draw() {
  for(int x = 0; x <= width; x += 20) {
    rect(x, 0, 10, 10);
  }
}
```

Una serie di quadrati vengono disegnati per tutta la larghezza della finestra.

[![Processing loop nesting #1](/assets/images/Processing_loop_nesting_1-1024x800.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_loop_nesting_1.png)

Facciamo la stessa cosa in verticale. Per comodità ho lasciato anche il codice di prima, commentandolo:

```java
void setup() {
  size(700, 500);
  background(255);
}

void draw() {
  /* Disegna i quadrati in orizzontale
  for(int x = 0; x <= width; x += 20) {
    rect(x, 0, 10, 10);
  }
  */
  for(int y = 0; y <= height; y += 20) {
    rect(0, y, 10, 10);
  }
}
```

[![Processing loop nesting 2](/assets/images/Processing_loop_nesting_2-1024x800.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_loop_nesting_2.png)

A questo punto uniamo le due cose:

```java
void setup() {
  size(700, 500);
  background(255);
}

void draw() {
  for(int x = 0; x <= width; x += 20) {
    for(int y = 0; y <= height; y += 20) {
      rect(x, y, 10, 10);
    }
  }
}
```

[![Processing loop nesting 3](/assets/images/Processing_loop_nesting_3-1024x800.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_loop_nesting_3.png)

Per ogni quadrato sull'asse _x_ viene disegnata per intero la colonna.

Per concludere il post di oggi, aggiungiamo un po' di psichedelia: copiando e incollando il codice qui sotto i colori cambieranno a ogni ciclo di _draw()_.

```java
void setup() {
  size(700, 500);
  background(255);
}

void draw() {
  for(int x = 5; x <= width; x += 20) {
    for(int y = 5; y <= height; y += 20) {
      fill(random(255), 0, random(255));
      rect(x, y, 10, 10);
    }
  }
}
```

[![Processing_loop_nesting_4](/assets/images/Processing_loop_nesting_4-1024x800.png)](https://blog.federicopepe.com/wp-content/uploads/2015/11/Processing_loop_nesting_4.png)
