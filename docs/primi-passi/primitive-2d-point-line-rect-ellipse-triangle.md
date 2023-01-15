---
title: "Primitive 2D: point(), line(), rect(), ellipse(), triangle()"
---

Nel [capitolo precedente](/primi-passi/schermo-pixel-e-linee) abbiamo realizzato il nostro primo sketch disegnando una linea sullo schermo in Processing. Proseguiamo il nostro percorso con una panoramica sulle altre forme di base, chiamate primitive 2D, che utilizzeremo di frequente nei nostri programmi futuri.

Cominciare a imparare a memoria i nomi delle funzioni che usiamo maggiormente e la loro sintassi corretta è di fondamentale importanza quando si impara a programmare. Talvolta, però, può capitare di avere dei dubbi e di non essere sicuri al cento per cento della sintassi o dei parametri di una funzione.

Se vi trovate in questa situazione, anziché andare per tentativi e perdere tempo inutilmente, consiglio di andare a dare un'occhiata nel **Reference**.

## Reference: la nostra guida

Sul sito di Processing all'indirizzo [https://processing.org/reference/](https://processing.org/reference/) trovate l'elenco di tutte le funzioni disponibili in questo linguaggio, cliccando su una di esse – potete provare, ad esempio, a cliccare su [_line()_](https://processing.org/reference/line_.html) – troviamo il dettaglio di quella funzione: _nome, esempi, descrizione, sintassi e parametri_.

![Uno screenshot che mostra la barra del menu all'interno di Processing in cui è selezionata la voce Help e vengono mostrate tutte le voci nel relativo sottomenu: Environment, Reference, Find in Reference, Getting Started, Troubleshooting, Frequently Asked Question, The Processing Foundation, Visit Processing.org](/assets/img/Processing-Reference-1024x393.png) 

Se non abbiamo accesso a internet, quando installiamo Processing sul nostro computer viene copiata sul nostro hard disk anche una copia completa e aggiornata del Reference. Per aprirla è sufficiente cliccare sul menu `Help > Reference`

Un altro trucco che ci permette di velocizzare molto il lavoro di ricerca è l'utilizzo del _Find in Reference_. Se stiamo lavorando a uno sketch e abbiamo già scritto del codice, evidenziando il nome della funzione su cui abbiamo dei dubbi possiamo cliccare su `Help > Find in Reference` – su Mac abbreviato con `⇧⌘F` (Shift + Command + F) – per accedere direttamente alla pagina del manuale che tratta di quella funzione specifica.

### Come leggere il reference

La documentazione è disponibile solo in inglese ma, con un piccolo sforzo, non è difficile carpire le informazioni che ci interessano.

Quando clicchiamo su una funzione, troviamo le seguenti sezioni:

- **Name**: viene riportato il nome della funzione.
- **Examples**: con poche righe di codice e delle immagini ci vengono mostrati degli esempi di funzionamento.
- **Description**: in modo più o meno dettagliato in base alla complessità della funzione, viene descritto il suo funzionamento e i parametri accettati. Nel caso di line(), vengono indicate anche altre funzioni che possiamo usare in concomitanza con la prima per, ad esempio, colorare la nostra linea.
- **Syntax**: la sintassi corretta per la funzione. Alcune funzioni possono accettare un numero diverso di parametri – nel caso di line() _quattro_ se stiamo lavorando in 2D oppure _sei_ nel caso in cui il nostro sketch sia in 3D – che portano, ovviamente, a risultati diversi.
- **Parameters**: i tipi di parametri che sono accettati. Questo sarà più chiaro quando parleremo, per l'appunto, di variabili e tipi di dati prossimamente.
- **Returns**: che tipo di dati la funzione restituisce in output. Anche in questo caso, sarà più chiaro quando tratteremo in modo più approfondito le funzioni.
- **Related**: le funzioni correlate a quella cercata.

## Primitive 2D

È arrivato il momento di disegnare un po' di primitive 2D. Per comodità utilizzerò sempre la funzione [_size()_](https://processing.org/reference/size_.html), che abbiamo [già incontrato precedentemente](/primi-passi/schermo-pixel-e-linee/), all'inizio di ogni sketch per impostare la dimensione della finestra a 500 pixel di altezza e larghezza.

### Punto – point()

![Uno screenshot di uno sketch di Processing con lo sfondo grigio e un punto nero al centro dello sketch](/assets/img/sketch_150728b_Processing_point-988x1024.png)

La funzione _point()_ disegna un punto di dimensione pari a 1 pixel sullo schermo. Quando lavoriamo in 2D, accetta due parametri: **x** e **y** che sono, rispettivamente, la coordinata orizzontale e quella verticale.

```java
size(500, 500);
point(250, 250);
```

Il punto, di colore nero, è stato disegnato al centro della finestra nella posizione _x = 250_ e _y = 250_. Data la dimensione ridotta del pixel sullo schermo, è possibile che facciate fatica a vederlo.

### Linea – line()

![Uno screenshot di uno sketch di Processing con lo sfondo grigio una linea nera disegnata](/assets/img/Processing_line-988x1024.png)

Della funzione _line()_ abbiamo già discusso ma, per completezza, non potevo escluderla da questo post. A differenza di point(), per disegnare una linea abbiamo bisogno di quattro parametri: x e y del punto di partenza e di arrivo.

```java
size(500, 500);
line(100, 150, 400, 250);
```

### Rettangolo – rect()

_rect()_ è la funzione che ci permette di disegnare un rettangolo sullo schermo. Se per disegnare un punto occorrevano due parametri e per una linea ne sono serviti quattro, potreste pensare che per il rettangolo ne servano almeno otto, due parametri x e y per ogni angolo. Ma non è così! Se, infatti, avessimo le coordinate dei quattro punti sarebbe comunque difficile stabilire quale punto deve essere collegato al seguente e questo ci causerebbe forti mal di testa.

La funzione rect(), quando si lavora in 2D, ha bisogno sempre di quattro parametri: _x_ e _y_ del punto di origine e poi larghezza e altezza del rettangolo.

```java
size(500, 500);
rect(250, 250, 100, 150);
```

Queste due linee di codice si possono quindi tradurre in:

- Imposta la misura della finestra: 500 pixel in altezza e 500 in larghezza
- Disegna un rettangolo il cui punto di origine sia x = 250, y = 250, largo 100 pixel e alto 150 pixel.

Ecco l'immagine che verrà prodotta:

![Uno screenshot di uno sketch di Procesing con lo sfondo grigio e un rettangolo bianco con bordo nero disegnato in basso a destra](/assets/img/sketch_150728b_Processing_rect-988x1024.png)

Come avrete sicuramente notato, così come per lo schermo il punto di origine è sempre l'angolo in alto a sinistra, anche per i rettangoli viene considerato di default come punto di origine lo stesso angolo della forma. Se vogliamo modificare questo comportamento esiste una funzione chiamata **_[rectMode()](https://processing.org/reference/rectMode_.html)_**_._ 

Modifichiamo leggermente il codice precedente:

```java
size(500, 500);
rectMode(CENTER);
rect(250, 250, 100, 150);
```

Ed ecco come cambia il risultato:

![Uno screenshot di uno sketch di Procesing con lo sfondo grigio con disegnato lo stesso rettangolo dell'immagine precedente ma, questa volta, allineato al centro della finestra](/assets/img/sketch_150728d_Processing_rectMode-988x1024.png)

Dal momento che il computer esegue in ordine un'operazione alla volta, dobbiamo ovviamente impostare rectMode() _prima_ di disegnare il rettangolo, altrimenti l'istruzione verrà ignorata.

Se volessimo disegnare un **quadrato**, è sufficiente utilizzare la funzione rect() impostando larghezza e altezza del rettangolo di pari dimensioni.

### Ellisse – ellipse ()

Con lo stesso principio usato per rect() possiamo usare la funzione _ellipse()_ per disegnare ellissi e cerchi. Anche questa funzione accetta quattro parametri: x e y del punto di origine e larghezza e altezza dell'ellisse (nel caso siano uguali, verrà disegnato un cerchio).

```java
size(500, 500);
ellipse(250, 250, 150, 150);
```

![Uno screenshot di uno sketch di Procesing con lo sfondo grigio con disegnato un cerchio bianco con bordo nero al centro della finestra](/assets/img/sketch_150728e_Processing_ellipse-988x1024.png)

Da notare che esiste la funzione _**[ellipseMode()](https://processing.org/reference/ellipseMode_.html)**_ ma, a differenza dei rettangoli, di default il punto di riferimento degli ellissi e dei cerchi è sempre il centro della forma.

### Triangolo – triangle()

Infine la funzione _triangle()_ ci permette di disegnare un triangolo indicando come parametri le coordinate x e y dei tre vertici del triangolo.

```java
size(500, 500);
triangle(250, 200, 300, 300, 200, 300);
```

![Uno screenshot di uno sketch di Procesing con lo sfondo grigio con disegnato un triangolo bianco con bordo nero al centro della finestra](/assets/img/sketch_150728f_Processing_triangle-988x1024.png)

Queste sono le forme che utilizzeremo maggiormente nei nostri prossimi esercizi. Come indicato nel reference, tra le primitive 2D ci sono altre due funzioni: **[quad()](https://processing.org/reference/quad_.html)** e **[arc()](https://processing.org/reference/arc_.html)** che in questo momento non è il caso di approfondire.
