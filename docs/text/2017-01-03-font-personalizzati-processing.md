---
title: "Font personalizzati: aggiungerli e utilizzarli"
date: "2017-01-03"
categories: 
  - "processing-text"
tags: 
  - "createfont"
  - "pfont"
  - "textfont"
coverImage: "Multiple-custom-fonts-in-processing.png"
---

In Processing è possibile utilizzare le font che abbiamo installato sul nostro computer all'interno dei nostri sketch. In questo post vedremo come aggiungerli al nostro programma e come utilizzarli in modo efficace. Questi argomenti saranno sicuramente utili a chi ha un background di tipo grafico e utilizza regolarmente Photoshop o Illustrator.

## Font vettoriali

La prima funzione che dobbiamo usare per aggiungere le font è **createFont()**, necessaria per convertire un file in formato _TrueType (.ttf)_ oppure _Open Type_ (_.otf_) in modo tale da poter essere utilizzato con la funzione [_text()_ di cui abbiamo parlato](https://blog.federicopepe.com/2016/11/testi-processing/).

Per vedere tutte le font installate compatibili, [come indicato anche nell'esempio nel reference](https://processing.org/reference/createFont_.html), basta scrivere le seguenti righe di codice:

String\[\] fontList = PFont.list();
printArray(fontList);

Queste due righe non fanno altro che generare e mostrare in console un'array di stringhe con tutti i nomi delle font attualmente installate sul computer:

\[0\] "Serif"
\[1\] "SansSerif"
\[2\] "Monospaced"
\[3\] "Dialog"
\[4\] "DialogInput"
...
\[862\] "Verdana"
\[863\] "Verdana-Bold"
\[864\] "Verdana-BoldItalic"
\[865\] "Verdana-Italic"

Ora che sappiamo quali font è possibile usare, dobbiamo convertirle. È necessario utilizzare un _data type_ specifico per salvare tutte le informazioni relative ai caratteri: **PFont**.

Creiamo una variabile di tipo **PFont** e usiamo la funzione **createFont()** per convertire il formato utilizzando due parametri: il primo è il nome della font, il secondo la grandezza di base.

Con la funzione **textFont()** diciamo al programma quale font usare.

```java
// Rimuovi il commento per vedere l'elenco delle font installate.
// String[] fontList = PFont.list();
// printArray(fontList);

PFont gill;

void setup() {
  size(500, 200);
  gill = createFont("GillSans", 28);
  textFont(gill);
  fill(0);
  text("Questo è un testo in GillSans", 10, height/2);
}

void draw() {
}
```

Questo il risultato:

[![Custom Font in Processing](/assets/images/Font-Processing-Adding_and_using-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2017/01/Font-Processing-Adding_and_using.png)

Nel caso volessimo usare più font all'interno del nostro programma, è sufficiente ripetere il processo con tutte i caratteri che vogliamo:

```java
// Rimuovi il commento per vedere l'elenco delle font installate.
// String[] fontList = PFont.list();
// printArray(fontList);

PFont gill, openSans;

void setup() {
  size(500, 200);
  gill = createFont("GillSans", 28);
  openSans = createFont("OpenSans", 28);
  textFont(gill);
  fill(0);
  text("Questo è un testo in GillSans", 10, height/2);
  textFont(openSans);
  text("Questo è un testo in OpenSans", 10, height/2 + 40);
}

void draw() {
}
```

[![Multiple custom fonts in Processing](/assets/images/Multiple-custom-fonts-in-processing-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2017/01/Multiple-custom-fonts-in-processing.png)
