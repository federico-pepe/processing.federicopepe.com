---
title: "Testi in Processing: text(), textSize() e textAlign()"
date: "2016-11-11"
categories: 
  - "processing-text"
tags: 
  - "text"
  - "textalign"
  - "textsize"
coverImage: "Testi-in-Processing_textAlign.png"
---

È possibile utilizzare Processing non solo per disegnare forme, colori e animazioni sullo schermo ma anche per lavorare con testi. Avere pieno controllo delle parole sullo schermo può essere utile in diversi progetti in particolare, per esperienza personale, nelle visualizzazioni di dati dove la giusta combinazione di grafica e testo può rendere le nostre infografiche più comprensibili.

## Visualizzare un testo: text()

La prima funzione da imparare è _**text()**._ Il suo funzionamento è piuttosto semplice; i parametri accettati sono tre: il carattere o la stringa che vogliamo scrivere e la posizione x e y.

```java

size(500, 200);
text("Questo è un testo", 10, height/2);
```

[![Funzione text() in Processing](/assets/images/Testi-in-Processing_1-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2016/11/Testi-in-Processing_1.png)

Di default il testo è di colore bianco e l'allineamento è a sinistra. Come per le forme, per modificare il colore è sufficiente utilizzare la funzione _fill()_.

```java
size(500, 200);
fill(0);
text("Questo è un testo", 10, height/2);
```

## [![Colorare i testi in processing con fill()](/assets/images/Testi-in-Processing_2-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2016/11/Testi-in-Processing_2.png)

È importante notare che la stringa all'interna della funzione deve essere scritta tra virgolette. Ovviamente è possibile passare alla funzione anche una variabile di tipo String.

```java
String testo = "Questo è un testo in una variabile";
size(500, 200);
fill(0);
text(testo, 10, height/2);
```

[![Utilizzare una variabile per il testo](/assets/images/Testi-in-Processing_3-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2016/11/Testi-in-Processing_3.png)

## Cambiare la dimensione del testo: textSize()

La funzione _**textSize()**_ imposta la grandezza della font. Una volta impostata, tutti i testi rappresentati al di sotto di questa funzione, avranno la stessa dimensione.

```java
String testo = "Questo è un testo in una variabile";
size(500, 200);
fill(0);
text(testo, 10, 25);
textSize(18);
text(testo, 10, 50);
text(testo, 10, 100);
textSize(12);
text(testo, 10, 125);
```

[![textSize() per modificare la dimensione](/assets/images/Testi-in-Processing_4-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2016/11/Testi-in-Processing_4.png)

## Allineare il testo: textAlign()

L'ultimo controllo di base di cui abbiamo bisogno è la funzione _**textAlign()**_ che ci permette di allineare il testo che stiamo mostrando sullo schermo. I parametri accettati sono _CENTER_, _LEFT_ o _RIGHT_ scritti rigorosamente in maiuscolo.

```java
size(500, 200);
line(width/2, 0, width/2, height);
fill(0);
textAlign(CENTER);
text("Testo allineato al centro", width/2, 50);
textAlign(LEFT);
text("Testo allineato a sinistra", width/2, 100);
textAlign(RIGHT);
text("Testo allineato a destra", width/2, 150);
```

[![Processing: textAlign()](/assets/images/Testi-in-Processing_textAlign-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2016/11/Testi-in-Processing_textAlign.png)

La stessa funzione accetta anche un secondo parametro per regolare l'allineamento verticale: _TOP, CENTER, BOTTOM._

Ecco l'esempio:

```java
size(500, 200);
fill(0);
textAlign(CENTER, TOP);
line(0, 50, width, 50);
text("Allineamento verticale top", width/2, 50);
textAlign(CENTER, CENTER);
line(0, 100, width, 100);
text("Allineamento verticale centrato", width/2, 100);
textAlign(CENTER, BOTTOM);
line(0, 150, width, 150);
text("Allineamento verticale bottom", width/2, 150);
```

[![textAlign() verticale: top, center, bottom](/assets/images/Testi-in-Processing_textAlign_verticale-1024x559.png)](https://blog.federicopepe.com/wp-content/uploads/2016/11/Testi-in-Processing_textAlign_verticale.png)

Per oggi è tutto, nel prossimo post vedremo insieme come modificare le font.
