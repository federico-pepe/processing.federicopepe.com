---
title: "sin() e cos(): onde e funzioni cicliche"
date: "2016-07-21"
categories: 
  - "processing-math"
tags: 
  - "cos"
  - "sin"
coverImage: "Processing_Angoli_sin.png"
---

Rimaniamo nel campo della trigonometria e analizziamo le funzioni `sin()` e `cos()` che, rispettivamente, ci consentono di calcolare il _seno_ e il _coseno_ di un angolo.

Entrambe le funzioni necessitano di un solo parametro: la misura di un angolo [espressa in radianti](https://blog.federicopepe.com/2016/07/angoli-randians-e-degree/) e restituiscono un numero _float_ il cui valore è sempre compreso tra -1.0 e 1.0.

Con questo snippet di codice potete verificare voi stessi nella console di Processing:

for(int angle = 0; angle < 360; angle++) {
 println(sin(radians(angle)));
}

Entrambe queste funzioni sono importanti per due motivi: restituendo valori compresi tra -1.0 e 1.0 è possibile sfruttarle per controllare altri parametri all'interno di uno sketch, il secondo è che sono funzioni cicliche.

## Esempi utilizzo funzione sin()

### Esempio 1:

![Processing, funzione sin()](/assets/images/Processing_Angoli_sin-1024x673.png)

L'immagine qui sopra è generata utilizzando questo codice:

```java
/*
 * Angoli II: sin() e cos()
 * by Federico Pepe
 *
*/

void setup() {
  size(640, 360);
  background(255);
  fill(0);
  noStroke();
}

void draw() {
  float angle = 0;
  
  for(int x = 0; x <= width; x+=5) {
    float y = height/2 + (sin(radians(angle))*35);
    rect(x, y, 2, 4);
    angle += 10;
  }
 
}
```

Non credo che il codice abbia bisogno di molte spiegazioni: con un semplice ciclo for, disegniamo dei piccoli rettangoli la cui posizione è determina dal ciclo for stesso, per il valore di x e, per quanto riguarda la y, da un valore calcolato con la funzione _sin()_. Ovviamente a ogni ciclo for dobbiamo incrementare la variabile **angle**.

### Esempio 2: controllo di altri parametri

Come dicevo prima, le cose si fanno più interessanti quando sfruttiamo il valore ciclico del seno all'interno di draw() per controllare altri parametri:

![Animazione utilizzando sin()](/assets/images/Processing_sin_animato-2.gif)

```java
/*
 * Sin() with Circle
 * by Federico Pepe
 *
 */
float angle = 0;
float diameter;

void setup() {
  size(500, 500);
}

void draw() {
  background(255);
  diameter = sin(angle)*200;
  ellipse(width/2, height/2, diameter, diameter);
  angle += 0.1;
}
```

In questo esempio animato, ad esempio, utilizziamo la funzione sin() per controllare la grandezza del cerchio in modo ciclico. Se avessimo incrementato la variabile diameter in modo standard `diameter++`, avremmo dovuto inserire un controllo if per determinare la grandezza massima e per far cambiare segno al valore... insomma un sacco di righe di codice in più.

### Esempio 3

Basta una piccolissima modifica al codice per ottenere un effetto completamente diverso:

![Processing sin() e cos()](/assets/images/Processing_sin_cos_animato-1.gif)

```java
/*
 * Sin() e Cos() with Circle
 * by Federico Pepe
 *
 */
float angle = 0;
float sin, cos;

void setup() {
  size(500, 500);
}

void draw() {
  background(255);
  sin = sin(angle)*200;
  cos = cos(angle)*200;
  ellipse(width/2, height/2, sin, cos);
  angle += 0.1;
}
```

Queste funzioni sono così divertenti da usare che potrei fare molti esempi; l'obiettivo di oggi era comunque darvi un'idea delle potenzialità e lasciarvi la possibilità di sperimentare liberamente. Come al solito, se volete potete lasciare un commento con le vostre animazioni!
