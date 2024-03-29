---
title: "Libreria Nice Color Palettes per Processing"
date: "2021-02-22"
categories: 
  - "colors"
  - "processing-libs"
tags: 
  - "colors"
  - "librerie"
  - "nice-color-palettes"
  - "palette"
  - "processing"
coverImage: "nice-color-palette.png"
---

Quasi due anni fa ho sviluppato la mia prima libreria per Processing chiamata **Nice Color Palettes**_._ Più che sviluppata da zero sarebbe meglio dire che ho effettuato il _porting_ in Java della libreria _[nice-color-palettes](https://github.com/Jam3/nice-color-palettes)_ sviluppata in javascript da [Matt Deslauriers](https://www.mattdesl.com).

Non ho idea del perché abbia fatto passare due anni prima di scriverne. Ma eccoci qua.

Come, [forse](https://blog.federicopepe.com/2017/08/palette-colori-da-immagine/), avrete [capito](https://blog.federicopepe.com/2020/05/creare-delle-palette-di-colori-in-modo-casuale/), sono ossessionato dai colori e dal trovare delle combinazioni che stanno bene insieme. Per mia e nostra fortuna esistono alcuni siti o applicazioni come [Coolors.co](https://coolors.co) o [Adobe Color](https://color.adobe.com) che ci aiutano nella ricerca della palette perfetta.

Uno dei primi siti a fare questo è stato [Colour Lovers](https://www.colourlovers.com) che, si dà il caso, abbia anche un'[API](https://www.colourlovers.com/api) che può essere interrogata per sapere quali sono le palette di colori più votate dagli utenti.

L'idea alla base di questa libreria era avere un modo rapido di accedere a varie combinazioni di colori che, tecnicamente, funzionano bene per usarle subito all'interno dei miei sketch.

## Installazione

La libreria può essere [scaricata direttamente da GitHub](https://github.com/federico-pepe/nice-color-palettes/releases) e installata trascinando i file all'interno della cartella _libraries_ di Processing. Oppure potete più semplicemente aprire Processing, cliccare nel menu _Sketch > Importa Libreria > Aggiungi Libreria_.

Nella finestra che si apre, cercate **Nice Color Palette** nel campo di ricerca, la selezionate e cliccate _Install_.

[![Installare la libreria Nice Color Palettes](assets/images/Schermata-2021-02-22-alle-21.38.24-1024x931.jpg)](https://blog.federicopepe.com/wp-content/uploads/2021/02/Schermata-2021-02-22-alle-21.38.24.jpg)

## Come usare Nice Color Palettes

Come prima cosa nel nostro sketch dobbiamo importare la libreria. Di solito l'importazione delle librerie esterne viene fatta come prima cosa nei programmi

```
import nice.palettes.*;
```

Dopodiché bisogna dichiarare l'oggetto di tipo **ColorPalette**. In questo caso gli ho assegnato il nome _palette_ ma, ovviamente, potete scegliere quello che più vi piace.

```
ColorPalette palette;
```

Ora, all'interno del ciclo di setup, dobbiamo fare l'inizializzazione

```
palette = new ColorPalette(this);
```

### Ottenere una palette di colori in modo casuale

A questo punto possiamo chiamare la funzione _getPalette()_ presente all'interno della libreria per ottenere un array di cinque colori scelti casualmente tra i 100 più votati sul sito Colour Lovers

```
import nice.palettes.*;
ColorPalette palette;

void setup() {
  palette = new ColorPalette(this);
  printArray(palette.getPalette());
  noLoop();
}

void draw() {
}
```

Il risultato in console sarà simile a questo:

\[0\] -12501430
\[1\] -9215378
\[2\] -5013116
\[3\] -1002338
\[4\] -531266

Ricordatevi che gli array iniziamo sempre a contare da zero. Purtroppo questi numeri non ci dicono molto, quindi realizziamo subito un programma che ci mostri il risultato visivamente

```
import nice.palettes.*;

ColorPalette palette;

void setup() {
  size(500, 500);
  noStroke();
  palette = new ColorPalette(this);
  palette.getPalette();
  
  for(int i = 0; i < 5; i++) {
    fill(palette.colors[i]);
    rect(i * width/5, 0, width/5, height);
  }
  
  noLoop();
}

void draw() {
}
```

Otterremo qualcosa simile a questo

[![](assets/images/Schermata-2021-02-22-alle-21.52.23-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2021/02/Schermata-2021-02-22-alle-21.52.23.jpg)

Siccome le palette sono caricate in modo casuale, ogni volta che premeremo _Run_ il risultato sarà diverso.

### Ottenere una palette specifica

Per ottenere una palette specifica, è sufficiente passare un parametro numerico alla nostra funzione _getPalette()_

Sostituendo, ad esempio, nel codice qui sopra la riga palette.getPalette(); con:

```
palette.getPalette(5);
```

Otterremo sempre la stessa combinazione di colori

## Altre funzioni della libreria

È possibile usare la funzione _getPaletteCount()_ per ottenere il numero di palette disponibili.

```
println(palette.getPaletteCount());
```

oppure accedere direttamente all'array di colori presenti dentro l'oggetto:

```
palette.colors[0];
```

Ricordatevi che l'array contiene _sempre_ 5 elementi per cui se scrivete _palette.colors\[5\];_ restituirà un errore.

Infine è possibile fare un refresh delle palette dal sito:

```
palette.refresh();
```

Di default questa funzione restituisce 20 valori ma è possibile arrivare fino a 100 (limite massimo dell'API) passando questo valore come parametro:

```
palette.refresh(100)
```

La libreria è pensata per funzionare anche in assenza di connessione a internet perché, al suo interno, contiene un file **.json** con 100 palette di colori.
