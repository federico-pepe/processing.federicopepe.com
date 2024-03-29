---
title: "Random e Perlin Noise"
date: "2016-06-01"
categories: 
  - "processing-math"
tags: 
  - "noise"
  - "perlin-noise"
  - "random"
---

In passato abbiamo [utilizzato la funzione](https://blog.federicopepe.com/2015/09/println-e-random/) _random()_ per rendere più interessanti i nostri sketch. Per fare un breve ripasso: vi ricordo che tale funzione accetta uno o due argomenti e restituisce sempre un numero casuale di tipo float. `random(10);` darà come risultato un numero compreso tra 0 e 10 mentre `random(5, 10);` restituirà un valore casuale compreso tra un minimo (5) e un massimo (10).

Random è una funzione bellissima perché, se usata nel modo giusto, può generare risultati davvero particolari senza complicare troppo il codice. Il problema a cui andiamo incontro, però, è che utilizzando questa funzione perdiamo il controllo del nostro sketch perché ci affidiamo completamente alla casualità: spesso i risultati possono sembrare molto caotici e privi di senso.

Ecco che in alcuni casi la funzione **noise()** ci può aiutare a creare una casualità "controllata".

## Cos'è il Perlin Noise?

Senza andare troppo nel dettaglio, il _Perlin Noise_ prende il nome da [Ken Perlin](http://mrl.nyu.edu/~perlin/), un professore di informatica della New York University che negli anni '80 ha sviluppato questa tipo di _rumore_ per generare texture in modo procedurale. I risultati della sua ricerca hanno reso possibile, nel campo della computer graphics, la rappresentazione della complessità della natura attraverso risultati organici generati da un algoritmo.

_**Aggiornamento 2.06.2016:** se siete interessati a capire meglio e in modo davvero approfondito come funziona il Perlin Noise, consiglio la lettura di [questo articolo (in inglese)](https://eev.ee/blog/2016/05/29/perlin-noise/)._

Nel [manuale di Processing](https://processing.org/reference/noise_.html) si trova un'informazione molto importante in merito a questa funzione:

> In contrast to the random() function, Perlin noise is defined in an infinite n-dimensional space, in which each pair of coordinates corresponds to a fixed semi-random value (fixed only for the lifespan of the program). The resulting value will always be between 0.0 and 1.0.

A differenza della funzione _random()_, _noise()_ restituirà un risultato **sempre compreso tra 0 e 1**. Teniamo a mente questa informazione e facciamo un esempio pratico.

## Random

```java
// Random e Perlin Noise

void setup() {
  size(500, 500);
}

void draw() {
  background(255);
  float x = random(width);
  ellipse(x, height/2, 50, 50);
}
```

Questo programma mostrerà un cerchio con posizione x totalmente casuale e y pari alla metà dell'altezza della finestra. **Nota:** Possiamo ridurre la velocità di esecuzione con la funzione [_frameRate()_](https://blog.federicopepe.com/2016/05/modulo-e-probabilita/).

Ecco l'output grafico in formato GIF:

![Utilizzo della funzione random in Processing](/assets/images/Processing_random.gif)

Prima di passare all'esempio con la funzione _noise()_ è necessario fare un'altra precisazione. Entrambe le funzioni che stiamo analizzando sono strettamente legate al concetto di tempo: _random()_ genera un nuovo valore casuale ogni volta che viene chiamata la funzione quindi, nell'esempio precedente, 60 volte al secondo; _noise()_, invece, riesce a generare risultati organici perché ciascun valore è legato temporalmente a quello precedente e al successivo.

Possiamo simulare lo scorrimento del tempo utilizzando una variabile che incrementiamo a ogni ciclo di draw; più piccolo sarà l'incremento, maggiore sarà la vicinanza dei valori restituiti dalla funzione.

## Noise

```java
// Random e Perlin Noise

// Creiamo una variabile per simulare l'avanzamento del tempo
float time; 

void setup() {
  size(500, 500);
}

void draw() {
  background(255);
  /*
   * Dal momento che noise restituisce un valore compreso tra 0 e 1, moltiplico
   * il numero per la larghezza della finestra per ottenere un valore compreso tra
   * 0 e 500
  */
  float x = noise(time) * width;
  ellipse(x, height/2, 50, 50);
  // A ogni ciclo draw, aumentiamo la variabile di tempo
  time += 0.05;
}
```

Per rendere l'esempio il più chiaro possibile ed evitare di rendere questo post troppo verboso, ho inserito diversi commenti nel codice. Come prima, vi mostro l'output grafico in formato GIF:

![Utilizzo del Perlin Noise in Processing](/assets/images/Processing_noise.gif)

Grazie alle due immagini animato, è semplice notare quanto i movimenti del secondo cerchio siano più organici rispetto al precedente. Se volete fare degli esperimenti partendo dal mio esempio, vi consiglio di modificare l'incremento della variabile time.

Cosa succede se scriviamo `time += 1;` oppure `time += 0.01;`?
