# Array bidimensionali

In programmazione gli **Array** sono utili per archiviare in modo ordinato una serie di informazioni. Per chi avesse bisogno di un recap, [questo è l'articolo](https://blog.federicopepe.com/2016/01/array/) in cui ho introdotto il concetto di array e il loro utilizzo in Processing.

A volte può capitare di avere a che fare con informazioni che non possono essere rappresentate in un'unica dimensione. Per questo motivo abbiamo bisogno di una struttura di dati multidimensionale: un **array bidimensionale**, ovvero un array di array, ci permette di lavorare con facilità su dati di questo tipo.

Per fare un esempio, proviamo a pensare di rappresentare i quadrati neri e bianchi di una scacchiera utilizzando il valore 0 per i primi e 1 per i secondi.

Partiamo da un array monodimensionale:
```
int[] scacchiera = { 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1 };
```

Con questo array ho rappresentato tutti e 64 i tasselli ma non è chiara la struttura a righe e colonne tipica della scacchiera. Ecco che, invece, inserendo ciascuna riga in un array separato le cose migliorano sensibilmente:

```
int[][] scacchiera = { 
 {1, 0, 1, 0, 1, 0, 1, 0},
 {0, 1, 0, 1, 0, 1, 0, 1},
 {1, 0, 1, 0, 1, 0, 1, 0},
 {0, 1, 0, 1, 0, 1, 0, 1},
 {1, 0, 1, 0, 1, 0, 1, 0},
 {0, 1, 0, 1, 0, 1, 0, 1},
 {1, 0, 1, 0, 1, 0, 1, 0},
 {0, 1, 0, 1, 0, 1, 0, 1} };
```

Abbiamo costruito il nostro primo **array bidimensionale**.

## Dichiarazione e inizializzazione

Le regole da rispettare in merito alla dichiarazione e inizializzazione dell'array bidimensionale rimangono identiche rispetto a quanto già visto in passato: è necessario indicare il tipo di dato, il nome dell'array ed è fondamentale stabilire una grandezza iniziale.

Sempre prendendo come riferimento l'esempio della scacchiera, inizializziamo l'array bidimensionale con 8 valori per le righe e 8 per le colonne:

`int[][] scacchiera = new int[8][8];`

## Array bidimensionali e nested loop

I [loop annidati](https://blog.federicopepe.com/2015/11/loop-for-e-nesting/) sono il modo migliore per accedere a tutti i dati presenti in un array bidimensionale. Proviamo a disegnare la nostra scacchiera:

```java
/*
 * Array bidimensionali e scacchi
 * Federico Pepe, 19.02.2017
 * http://blog.federicopepe.com/processing
*/

int[][] scacchiera = { 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1}, 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1}, 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1}, 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1} };

void setup() {
  size(480, 480);
  
  int rows = 8;
  int cols = 8;
  
  for (int i = 0; i < rows; i++) {
    for(int j = 0; j < cols; j++) {
      if(scacchiera[i][j] == 0) {
        fill(0);
      } else {
        fill(255);
      }
      rect(i*60, j*60, 60, 60);
    }
  }
}

void draw() {
}
```

All'inizio del programma troviamo l'array bidimensionale che contiene i valori su cui dobbiamo lavorare. All'interno della funzione _setup()_ abbiamo impostato la grandezza della finestra e abbiamo creato due variabili per avere il numero di righe (_rows_) e il numero di colonne (_cols_).

Utilizzando due loop andiamo a vedere tutti i valori presenti all'interno dell'array: se il valore trovato è uguale a 0 la casella sarà nera, altrimenti bianca. Completiamo il programma andando effettivamente a disegnare la singola casella.

## Esercizio di difficoltà media

In questo script ci sono diversi parametri "hard-coded". Siete in grado di modificare lo script affinché, ad esempio, modificando i valori all'interno di size() mi venga disegnata sempre una scacchiera di 8x8 che occupi l'intera grandezza della finestra (anche quando non è quadrata)?

## Esercizio di difficoltà alta

Partendo dalla soluzione all'esercizio di difficoltà media, sareste in grado di modificarlo ulteriormente per fare in modo che la griglia non sia necessariamente 8x8?
