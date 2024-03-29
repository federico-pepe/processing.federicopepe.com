---
title: "Modificare le immagini: tint(), filter()"
date: "2017-03-19"
categories: 
  - "processing-images"
tags: 
  - "filter"
  - "tint"
coverImage: "Processing_tint_hexadecimal.png"
---

Proseguiamo l'approfondimento su Processing e immagini. Nell'era di Instagram siamo abituati a cambiare l'aspetto delle nostre foto prima di condividerle con gli altri. Le funzioni **tint()** e **filter()** – già incluse all'interno del linguaggio – ci consentono di alterare le immagini a nostro piacimento.

## La funzione tint()

Questa funzione consente di alterare il colore generale delle foto. L'effetto non è permanente tanto che invocando la funzione **noTint()** è possibile ritornare all'originale.

I parametri accettati vanno da uno a quattro [come specificato nel reference](https://processing.org/reference/tint_.html). Prendendo quest'immagine di partenza –chi non ama i gatti? – facciamo qualche esempio:

![](/assets/images/cat-300572_1280.jpg) Immagine di partenza, presa da [Pixabay](https://pixabay.com/p-300572/?no_redirect) (CC)

Passiamo alla funzione un solo parametro per applicare un filtro "grigio":

```java
/*
 * Immagini: tint(), filter() e masking
 * Federico Pepe, 19.03.2017
 * http://blog.federicopepe.com/processing
*/

PImage immagine;

void setup() {
  size(640, 535);
  immagine = loadImage("cat.jpg");
  tint(100);
  image(immagine, 0, 0);
}

void draw() {
 
}
```

![](/assets/images/Processing_tint_gray-1024x911.png)

Passiamo a tint() tre parametri: `tint(255, 255, 50);`. È possibile usare tre valori RGB che HSB in base alla funzione _colorMode()_ precedentemente impostata.

![Processing use tint()](/assets/images/Processing_tint_yellow-1024x911.png)

Se avete un background in web design, sappiate che Processing accetta anche valori esadecimali `tint(#FF55EE);`

![Processing tint hexadecimal](/assets/images/Processing_tint_hexadecimal-1024x911.png)

È possibile anche sfruttare il parametro della trasparenza _alpha._

```java
tint(#FF55EE, 70);
image(immagine, 0, 0);
tint(255, 255, 50, 50);
image(immagine, 0, 0);
```

Questo codice darà il seguente risultato:

![Processing tint e trasparenza](/assets/images/Processing_tint_with_alpha-1024x911.png)

## Aggiungere un filtro con la funzione filter()

Oltre alla funzione _tint()_, Processing ha al suo interno la funzione filter() che, come i comuni programmi di grafica come Adobe Photoshop o GIMP, permette di applicare dei filtri alle foto.

I parametri sono otto e devono essere sempre indicati in maiuscolo: THRESHOLD, GRAY, INVERT, POSTERIZE, BLUR, OPAQUE, ERODE e DILATE. Alcuni di essi accettano un secondo parametro mentre altri no.

Mentre la funzione _tint()_ doveva essere dichiarata prima di mostrare l'immagine, la funzione _filter()_ è inserita successivamente, come indicato nel seguente esempio:

```java
/*
 * Immagini: tint(), filter() e masking
 * Federico Pepe, 19.03.2017
 * http://blog.federicopepe.com/processing
*/

PImage immagine;

void setup() {
  size(640, 535);
  immagine = loadImage("cat.jpg");
  tint(100);
  image(immagine, 0, 0);
}

void draw() {
 
}
```

### THRESHOLD

Converte i pixel di un'immagine in bianco o nero in base alla soglia impostata che può assumere un valore compreso tra 0 e 1. Se non viene indicato, il valore di default è 0.5.

\[gallery link="file" size="medium" ids="1154,1155,1156"\]

### BLUR

Applica un filtro di sfocatura gaussiana. Il secondo parametro indica il raggio della sfocatura.

\[gallery size="medium" link="file" ids="1159,1160,1161"\]

### POSTERIZE

Limita ciascun canale dell'immagine al numero di colori passati come parametro. I valori accettati vanno da 2 a 255.

\[gallery link="file" size="medium" ids="1162,1163,1164"\]

### GRAY

Converte i colori dell'immagine nel loro valore corrispondente in scala di grigi.

### OPAQUE

Imposta il canale trasparenza (alpha) opaco.

### INVERT

Inverte il valore di ciascun pixel.

### ERODE e DILATE

Il primo riduce le aree illuminate mentre il secondo le aumenta.

\[gallery link="file" columns="5" size="medium" ids="1165,1166,1167,1168,1169"\]

Le funzioni che abbiamo visto oggi sono solo l'inizio; prossimamente vedremo come creare i nostri filtri personalizzati andando a lavorare sui singoli pixel.
