---
title: "Trasformazioni: translate(), rotate(), scale()"
date: "2016-10-06"
categories: 
  - "processing"
tags: 
  - "rotate"
  - "scale"
  - "translate"
  - "trasformazioni"
coverImage: "Trasformazioni_translate_Processing_2.png"
---

Abbiamo già avuto modo all'inizio del percorso base di prendere esplorare il [sistema di coordinate](https://blog.federicopepe.com/2015/07/schermo-pixel-e-linee/) in Processing. Una cosa che non abbiamo affrontato in modo approfondito è che questo sistema non è statico. Esistono, infatti delle funzioni dette **trasformazioni** che ci permettono di modificare il nostro impianto di base. Tali funzioni sono _translate(), rotate()_ e _scale()_ che, come è chiaro dai loro nomi, ci permettono di traslare, ruotare e scalare le forme che rappresentiamo sullo schermo.

Perché usare le trasformazioni è utile? Semplicemente perché quando lavoriamo con geometria complesse è più semplice modificare una sola linea di codice per spostare una o più forme invece che ripensare nuovamente a tutte le coordinate. In poche parole, è un ottimo sistema per semplificarci la vita.

## translate()

La funzione translate sposta il punto di origine della nostra forma; accetta due parametri: le coordinate x e y del nostro spostamento. Ovviamente quando chiamiamo questa funzione, lo spostamento viene applicato per tutte le forme che vengono disegnate _dopo_ la funzione stessa.

```java
void setup() {
  size(500, 500);
  background(255);
}

void draw() {
  rect(50, 50, 200, 50);
  translate(50, 100);
  rect(50, 50, 200, 50);
}
```

[![Translate() in Processing](/assets/images/Trasformazioni_translate_Processing-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/10/Trasformazioni_translate_Processing.png)

Ecco che pur utilizzando le stesse coordinate per i due rettangoli, il secondo si trova spostato di 50 pixel verso destra e 100 più in basso.

Un particolare di questa funziona è che, se ripetuta, è incrementale:

```java
void setup() {
  size(500, 500);
  background(255);
}

void draw() {
  rect(50, 50, 200, 50);
  translate(50, 100);
  rect(50, 50, 200, 50);
  translate(50, 100);
  rect(50, 50, 200, 50);
}
```

In questo secondo esempio il terzo rettangolo risulta spostato, rispetto al primo, di 100 pixel verso destra e 200 in basso.

[![Translate() in processing è una funzione additiva](/assets/images/Trasformazioni_translate_Processing_2-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/10/Trasformazioni_translate_Processing_2.png)

Importante notare anche che pur essendo inserite all'interno di un ciclo draw(), a ogni loop l'intero sistema viene resettato.

## rotate()

La funzione _rotate()_ ruota il sistema di coordinate. Accetta un solo parametro, la quantità di rotazione che deve essere espresso in [radianti](https://blog.federicopepe.com/2016/07/angoli-randians-e-degree/). Le forme vengono sempre ruotate relativamente al punto di origine (0, 0) della finestra e non relativamente al punto di riferimento della forma. Se il parametro di rotazione è positivo, il movimento sarà in senso orario.

Esempio di rotazione di 45 gradi convertiti nel valore in radianti.

```java
void setup() {
  size(500, 500);
  background(255);
}

void draw() {
  rect(50, 50, 200, 50);
  rotate(radians(45));
  rect(50, 50, 200, 50);
}
```

[![Trasformazioni: rotate()](/assets/images/Trasformazioni_rotate-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/10/Trasformazioni_rotate.png)

## scale()

La funzione _scale()_ modifica il sistema di coordinate ingrandendo o rimpicciolendo le forme. Questa funzione accetta uno o due parametri: nel primo caso verrà applicato quel valore a tutte le dimensioni mentre, nel secondo, il primo scalerà l'asse x e il secondo l'y.

Per far funzionare la funzione _scale()_ correttamente i valori devono essere espressi in percentuale usando i numeri decimali: scrivendo 2 otterremo un incremento del 200%, scrivendo 0.5 la forma sarà rimpicciolita del 50%.

```java
void setup() {
  size(500, 500);
  background(255);
}

void draw() {
  fill(255);
  rect(50, 50, 200, 50);
  scale(0.5);
  fill(255, 0, 0);
  rect(50, 50, 200, 50);
}
```

[![Utilizzo di scale() in Processing](/assets/images/Trasformazioni_scale-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/10/Trasformazioni_scale.png)
