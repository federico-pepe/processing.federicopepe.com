# Array: dichiarazione, inizializzazione e utilizzo

Avevo concluso l'[ultimo post](https://blog.federicopepe.com/2016/01/oop-classi-e-oggetti-parte-2/) relativo alla programmazione orientata agli oggetti con una domanda: _se volessimo creare decine o centinaia di oggetti?_ Il copia incolla non sarebbe certamente la scelta più consona.

Abbiamo capito già da tempo che uno dei principi di base della programmazione è scrivere meno righe di codice possibile per ottenere il risultato sperato. Introduciamo oggi il concetto di **array**.

## Cos'è un Array?

Nel post dedicato alle [variabili](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/) abbiamo parlato di come dichiararle e inizializzarle ma non ci siamo mai soffermati su una questione molto importante: una variabile può contenere **un solo valore**.

È vero che questo valore può variare in base all'andamento del nostro programma ma non è possibile, ad esempio, che una variabile di tipo integer possa valere contemporaneamente 5 e 10.

Gli array risolvono questo problema perché rappresentano una **lista di valori**: all'interno di un array io posso inserire una serie di valori, purché siano tutti dello stesso _data type_. Un altro importante vantaggio è che ciascun elemento ha un **ordine preciso** all'interno della lista che è identificato da un **indice univoco**.

È fondamentale ricordare che l'indice **parte sempre da** **0** di conseguenza se sto utilizzando un array che contiene 10 elementi, l'ultimo valore avrà un indice pari a 9.

Ricapitolo per chiarezza i punti chiave:

- Un array rappresenta una lista di elementi
- Gli elementi all'interno dell'array devono essere tutti dello stesso tipo
- Gli elementi all'interno dell'array hanno un ordine preciso
- Ciascun elemento è identificato da un indice univoco che parte sempre da 0

## Dichiarazione e creazione di un array

La sintassi per dichiarare un array è molto semplice: rispetto a quella utilizzata per le variabili, dobbiamo solo aggiungere delle parentesi quadre:

int[] myArray;

Con questa riga di codice ho dichiarato un array di nome _myArray_ che conterrà al suo interno una lista di valori di tipo integer. Non ho ancora detto al mio programma _quanti_ elementi conterrà questo array e, di conseguenza, la lista è ancora vuota.

Passiamo all'inizializzazione di myArray:

int[] myArray = new int[10];

Ho creato un'istanza di un nuovo array e ho gli ho assegnato una dimensione: la lista sarà composta da 10 elementi di tipo integer.

La grandezza dell'array può essere _hard-coded_ come nell'esempio qui sopra, oppure può essere una _variabile_ (di tipo integer) oppure un'espressione matematica che dia come risultato un _integer_:

```java
// Un array di integer con grandezza hard-coded
int[] myArray = new int[10];

// Un array di float con grandezza passata tramite variabile (integer)
int sizeOfArray = 5;
float[] mySecondArray = new float[sizeOfArray];

// Un array di oggetti "Car" con grandezza passata tramite funzione
Car[] cars = new Car[2+5];
```

## Inserire valori in un array

Non ci resta che cominciare a riempire il nostro array di informazioni.

Una prima opzione è quella di inserire le variabili specificando la posizione _indice_ di riferimento. Questa scelta, ovviamente, non è la più funzionale.

```java
// Dichiaro e inizializzo il mio array che conterrà 5 elementi di tipo integer
int[] myArray = new int[5];

myArray[0] = 5;   // Il primo elemento (indice = 0) sarà: 5
myArray[1] = 10;  // Il secondo elemento (indice = 1) sarà: 10
myArray[2] = 3;   // Il terzo elemento (indice = 2) sarà: 3
myArray[3] = 0;   // Il quarto elemento (indice = 3) sarà: 0
myArray[4] = 340; // Il quinto elemento (indice = 4) sarà: 340
```

Una seconda opzione è quella di inserire tutti i valori, separati da virgole, all'interno di parentesi graffe:

```java
// Dichiaro un array di tipo integer di nome myArray con all'interno i seguenti valori: 5, 10, 3, 0, 340

int[] myArray = {5, 10, 3, 0, 340};
```

Le due porzioni di codice qui sopra rappresentato, di fatto, la stessa identica lista.

## Operazioni matematiche con gli array

Per capire se tutto è chiaro, proviamo ad analizzare un problema: se volessimo creare una lista di 500 elementi contenenti numeri random compresi tra 0 e 255?

Per prima cosa non dobbiamo dimenticare che la funzione _random()_ restituisce valori di tipo _float_. Avendo già deciso che la nostra lista sarà composta da 500 elementi, possiamo anche inizializzare il nostro array:

float valori\[\] = new float\[500\];

Ora dobbiamo inserire tutti i valori; farlo uno ad uno sarebbe un massacro ma, per fortuna, abbiamo già studiato i cicli [while](https://blog.federicopepe.com/2015/11/loop-while/) e [for](https://blog.federicopepe.com/2015/11/loop-for-e-nesting/) il cui scopo è effettuare operazioni ripetitive.

Per comodità utilizzerò un ciclo for: posso usare la variabile del ciclo per indicare l'indice dell'array nel quale inserire il valore random:

```java
float valori[] = new float[500];

for(int i = 0; i < 500; i++) {
  valori[i] = random(255);
}

printArray(valori);
```

![Array e ciclo for](/assets/images/Array_For-1024x898.png)

Come si può notare nell'immagine, grazie alla funzione _printArray_ nella console visualizzo tutti i valori e il relativo indice all'interno dell'array.

Ovviamente è possibile accedere singolarmente a qualsiasi elemento indicando l'indice:

println("Il valore all'indice 306 è: "+ valori\[306\]);

## Debugging degli array e .length

Un errore in cui si può incorrere frequentemente quando si lavora con gli array è: _ArrayIndexOutOfBoundsExceptions._ Tale problema si verifica quando chiediamo al nostro programma di accedere a un valore ad un indice non presente nell'array.

Se modifichiamo il codice del ciclo for nel precedente esempio in questo modo:

for(int i = 0; i <= 500; i++)

riscontreremo proprio questo tipo di errore perché il ciclo si ripeterà finché il valore di _i_ sarà uguale a 500. Il problema è che la grandezza dell'array che ho dichiarato all'inizio è pari a 500 ma, partendo da 0, l'ultimo valore dell'indice è 499.

Per ovviare a questo problema possiamo usare una proprietà degli array: **.length**. In pratica, anziché dover ricordarsi quant'è la lunghezza di ogni array e, prossimamente, vedremo che questa potrebbe anche variare, diciamo al programma di capire da sé quant'è la lunghezza della nostra lista e di comportarsi di conseguenza.

Ecco che il codice finito potrebbe essere:

```java
float valori[] = new float[500];

for(int i = 0; i < valori.length; i++) {
  valori[i] = random(255);
}

printArray(valori);
```
