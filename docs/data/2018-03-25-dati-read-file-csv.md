---
title: "Leggere file CSV"
date: "2018-03-25"
categories: 
  - "data"
tags: 
  - "csv"
  - "dati"
  - "getcolumncount"
  - "getrowcount"
  - "loadstrings"
  - "loadtable"
  - "table"
coverImage: "Leggere-file-CSV.jpg"
---

Cominciamo il nostro percorso per imparare a lavorare con i dati: in questo post vedremo insieme come utilizzare i file di tipo CSV in Processing.

Per chi non conoscesse questo tipo di file o ci li avesse mai usati si tratta, in breve, di file di testo in cui i valori sono separati da virgole. CSV, infatti, sta per _comma separated values_. Nella maggior parte dei casi questi file vengono esportati da **Microsoft Excel**, uno dei programmi più diffusi (e odiati) per gestire tabelle di dati.

Per dare la possibilità a chiunque mi segua sul blog di seguire gli esercizi, utilizzerò **Google Sheet**, alternativa gratuita e accessibile via browser del blasonato programma di Microsoft.

Ecco, quindi, il nostro primo set di dati: le _statistiche metoclimatiche degli ultimi 10 anni (2008-2017) della regione Veneto_, prese dal sito del _[Mipaaf](https://www.politicheagricole.it/flex/FixedPages/Common/miepfy700_Osservatorio.php/L/IT)_ e portate su Google Sheet.

[Scarica i dati](https://docs.google.com/spreadsheets/d/1Gip2aLeaCLo_qlrZQuKhCfsVPjgPIUPt7Dm48KybRdk/)

Per esportare il file come CSV cliccate su _File > Scarica Come > Valori separati da virgola (.csv, foglio corrente)._ Di seguito le immagini di come si presenta il file prima e dopo l'esportazione:

\[caption id="attachment\_1477" align="aligncenter" width="1024"\][![Dati in Processing: File CSV in Google Sheet](images/File-CSV-in-Google-Sheet-1024x618.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/03/File-CSV-in-Google-Sheet.jpg) I dati visti in Google Sheet\[/caption\]

\[caption id="attachment\_1478" align="aligncenter" width="1024"\][![Dati in Processing: File CSV in Atom](images/File-CSV-in-Atom-1024x617.jpg)](https://blog.federicopepe.com/wp-content/uploads/2018/03/File-CSV-in-Atom.jpg) Gli stessi dati, esportati in CSV\[/caption\]

## Dati in un file CSV: semplice testo

Come dicevamo all'inizio, il file CSV esportato non è altro che un file di testo contenente dei valori. Per cominciare a leggerne il contenuto è sufficiente utilizzare la funzione **loadStrings()**: tale funzione accetta in input un file di testo e restituisce un array di stringhe.

Prima di procedere, consiglio di rinominare il file scaricato in _data.csv_. Non dimenticate di [trascinarlo all'interno della finestra di Processing](https://blog.federicopepe.com/2016/12/caricare-file-esterni-processing/) per aggiungerlo al nostro sketch.

```processing

/*
 * Leggere file CSV
 * Federico Pepe, 25.03.2018
 * http://blog.federicopepe.com/processing
 */

String[] csv;

void setup() {
  csv = loadStrings("data.csv");
  printArray(csv);
  noLoop();
}

void draw() {
}
```

Con queste poche righe di codice nella console ogni riga del file viene mostrata come un nuovo elemento dell'array di stringhe.

\[0\] "Descrizione,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017"
\[1\] "Temp. minima (°C),6.9,7.3,6.7,7.4,7.2,7.7,8.7,8,7.6,7.1"

Fino a qui niente di difficile ma a noi interessa accedere ai singoli valori presenti in ciascuna colonna. A questo punto ci torna utile riprendere gli [array bidimensionali](https://blog.federicopepe.com/2017/02/array-bidimensionali-processing/): un sistema che ci permette di rappresentare facilmente una struttura formata da righe e colonne, proprio come un file excel/csv.

Modifichiamo, dunque, il nostro codice come segue:

```processing
/*
 * Leggere file CSV
 * Federico Pepe, 25.03.2018
 * http://blog.federicopepe.com/processing
 */

String[] csv;
String[][] dati;

void setup() {
  csv = loadStrings("data.csv");
  dati = new String[csv.length][10]; 
  
  for(int i = 0; i < csv.length; i++) {
    dati[i] = csv[i].split(",");
    printArray(dati[i]);
  }
  
  noLoop();
}

void draw() {
}
```

Abbiamo aggiunto un array bidimensionale chiamato dati la cui dimensione è determinata dal numero di righe `[csv.length]` e dal numero di colonne meno uno perché si conta sempre da zero `[10]`.

Con un semplice ciclo for accediamo a tutte le righe del file e, utilizzando la funzione `.split(",")` separiamo tutti i valori che sono separati dalla virgola.

Affinché sia tutto il più chiaro possibile possiamo fare un po' di esperimenti con println inserendo nel primo valore dell'array il numero della riga e nel secondo quello della colonna.

`println(dati[3][2]);` restituisce il valore 0.7 che corrisponde, infatti, alla cella nella quarta riga "Scarto dal clima" e nella terza colonna "2009".

## Leggere file CSV in modo più semplice: Table

Siamo riusciti nel nostro intento ma credo sia ovvio che il metodo che abbiamo usato non sia il più congeniale.

Per nostra fortuna i creatori di Processing avevano già pensato a questa evenienza e hanno creato un oggetto specifico chiamato **[Table](https://processing.org/reference/Table.html)** che, come è facile intuire dal nome, rappresenta già una tabella completa di righe e colonne.

Grazie ai numerosi metodi disponibili per gli oggetti di tipo _Table_ è possibile lavorare con i dati in modo semplice e intuitivo.

Aggiorniamo il nostro codice:

```processing

/*
 * Leggere file CSV
 * Federico Pepe, 25.03.2018
 * http://blog.federicopepe.com/processing
 */

Table csv;

void setup() {
  csv = loadTable("data.csv", "header");

  println("Numero righe: " + csv.getRowCount());
  println("Numero colonne: " + csv.getColumnCount());
  
  for(int i = 0; i < csv.getRowCount(); i++) {
    println(csv.getFloat(i, 2));
  }
  
  noLoop();
}

void draw() {
}
```

Abbiamo sostituito i due array di stringhe con un oggetto di tipo Table chiamato csv. Attraverso la funzione **loadTable()** carichiamo i dati all'interno della variabile. Passando il parametro "header" stiamo dicendo a Processing di ignorare la prima riga del file che contiene l'intestazione.

Attraverso le funzioni **.getRowCount()** e **.getColumnCount()** accediamo al numero di righe e colonne del file e, infine, con il nostro ciclo for stampiamo in console i valori di tipo _float_ contenuti nella terza colonna (quindi quelli relativi al 2009).

## Conclusione

In questo post abbiamo messo molta carne al fuoco e abbiamo cominciato ad addentrarci nel mondo dei dati e dei file CSV. Assicuratevi di aver compreso bene tutte le funzioni e gli esempi inseriti in questo post prima di proseguire con la lettura del prossimo.
