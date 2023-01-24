# Variabili in Processing: creazione e personalizzazione

Abbiamo già incontrato il termine **variabile** un [paio di settimane](https://blog.federicopepe.com/2015/08/variabili-built-in/) fa quando avevo descritto, ad esempio, come utilizzare _mouseX_ e _mouseY_ per rendere i nostri sketch interattivi.

Come avevo scritto in quel post:

> le variabili sono dei parametri che possono assumere un valore che può essere cambiato durante l’esecuzione del programma attraverso, ad esempio, semplici funzioni matematiche.

Oggi impareremo a creare delle variabili personalizzate e capiremo come utilizzarle nei nostri programmi. Quella di oggi è una lezione di fondamentale importanza perché, come avrete modo di vedere, cambierà completamente il vostro modo di programmare.

## Creare delle variabili

Creare una variabile è un processo relativamente semplice. I passaggi che dobbiamo fare sono i seguenti:

1. Dichiarazione della variabile
    - Assegnazione di un data type
    - Assegnazione di un nome alla variabile
2. Inizializzazione della variabile
3. Utilizzo della variabile

In poche parole dobbiamo **dare un nome alla variabile**, dirgli che **tipologia di informazione** vogliamo che contenga e dobbiamo **assegnargli un valore iniziale**. Se questi passaggi sono fatti nel modo corretto (e, tra poco, vi spiegherò come fare), poi potremmo usare quelle variabili a nostro piacimento.

Partiamo da un esempio:

```java
int lunghezza;
lunghezza = 110;
```

Cosa abbiamo fatto con queste due linee di codice? Abbiamo creato una **variabile** di tipo **integer** (abbreviato in _int_) chiamata _lunghezza_ e l'abbiamo inizializzata assegnando un valore pari a _110_.

A una variabile possiamo assegnare il nome che vogliamo senza particolari restrizioni a patto che tale nome non sia già utilizzato dalla sintassi di Processing. La regola empirica per capire se possiamo utilizzare un nome che abbiamo scelto è: se il nome che assegnamo non cambia colore, non dovremmo avere problemi.

Una buona pratica da seguire è quella di dare un nome alle variabili che sia significativo e rifletta l'utilizzo che verrà fatto successivamente: questo renderà il nostro codice facilmente interpretabile anche a mesi o anni di distanza. Quindi, benché io possa nominare delle variabili _tizio_, _caio_, e _sempronio_ se quella variabile verrà utilizzata per definire la X di un ellisse è meglio chiamarla, ad esempio, _circleX._

Dal momento che il nome che assegniamo alle variabili deve essere un'unica parola, i programmatori utilizzano il cosiddetto [CamelCase](https://it.wikipedia.org/wiki/Notazione_a_cammello) per nominare variabili complesse. Nella pratica, si tratta di unire parole diverse tra loro lasciando le iniziali maiuscole (la prima lettera della variabile sempre minuscola). Ecco perché, vedendo dei programmi in Processing, troverete variabili come: **backgroundColor** oppure **radiusValue**, ecc...

Ultima nota sui nomi delle variabili: potendo scegliere liberamente le parole da utilizzare non c'è restrizione sulla lingua da utilizzare. Se volete rendere il vostro codice leggibile il più possibile, conviene ovviamente usare l'inglese.

## Tipi di dati

Assegnare il tipo di dato corretto è importante per evitare che il nostro programma smetta di funzionare e ci restituisca un errore. Se, infatti, il programma si aspetta di trovare un numero intero e riceve un numero decimale si bloccherà.

I principali tipi di dati sono:

- **integer**: abbreviato in _int_ e descrive un numero intero (es: 45)
- **float**: descrive un numero decimale (es: 34,20394)
- **char**: descrive un singolo carattere (es: 'A');
- **String**: descrive una sequenza di caratteri (es: 'Questa è una stringa')

Esistono anche altri tipi di dati e l'elenco completo può essere trovato nel Reference. Per il momento è sufficiente che impariate quelli descritti qui sopra.

## Scopo delle variabili

Le variabili non devono essere per forza dichiarate e inizializzate tutte all'inizio del nostro programma. Possiamo farlo tranquillamente mentre procediamo con la scrittura del codice. Dobbiamo, però, fare attenzione allo _scopo_ delle variabili ovvero in quale parte di codice verrà utilizzata.

Anche in questo caso, credo sia meglio partire da un esempio:

```java
int circleX; // dichiarazione

void setup() {
  size(400, 400);
  circleX = 100; // inizializzazione
}

void draw() {
  ellipse(circleX, 110, 50, 50); // utilizzo
}
```

In questo breve programma ho creato una variabile **circleX** di tipo integer all'inizio del programma, nel blocco di codice _setup()_ l'ho inizializzata assegnando un valore pari a 110 e l'ho utilizzata in _draw()_ per disegnare un cerchio. Se copiate e incollate il codice nell'editor di Processing e provate a farlo funzionare, non avrete alcun problema.

Ora cambiamo leggermente il nostro codice:

```java
int circleX; // dichiarazione

void setup() {
  size(400, 400);
  circleX = 100; // inizializzazione
  int circleY = 110; // dichiarazione e inizializzazione
}

void draw() {
  ellipse(circleX, circleY, 50, 50); // utilizzo
}
```

In questo secondo esempio ho fatto una piccola modifica: ho creato e inizializzato una variabile chiamata **circleY** all'interno della funzione _setup()_ e l'ho utilizzata all'interno della funzione _draw()_. Se proviamo a far partire questo programma, otterremo un errore **_Cannot find anything named "circleY"_**:

![Scopo delle variabili in Processing](/assets/images/Variabili_Processing_Scopo-880x1024.png)

Perché Processing non riesce a _trovare_ la variabile circleY pur essendo stata dichiarata e inizializzata? La differenza tra circleX e circleY è che la prima è una variabile **_pubblica_** mentre la seconda è **_privata_**. Cosa significa? Nel primo caso, essendo stata dichiarata all'inizio, circleX può essere usata ovunque all'interno del programma; circleY, invece, è stata dichiarata all'interno della funzione _setup()_ ma viene utilizzata dalla funzione _draw()_ e questo non è possibile. È come se ogni blocco di codice fosse un'entità privata a sé stante e le variabili che vengono dichiarate al suo interno non possono essere utilizzate dagli altri blocchi di codice.

Per far funzionare questo secondo esempio abbiamo due possibilità: spostare la dichiarazione di circleY all'inizio del programma – l'inizializzazione può, invece, rimanere all'interno di setup() o all'interno di draw() – oppure possiamo spostare la funzione ellipse() dentro il blocco di codice setup().

Nel prossimo post vedremo insieme come modificare una (o più) variabili, controllarne in ogni momento il valore e, attraverso esempi pratici, utilizzarle.
