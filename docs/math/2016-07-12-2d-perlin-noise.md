---
title: "2D Perlin Noise"
date: "2016-07-12"
categories: 
  - "processing-math"
tags: 
  - "2d"
  - "loadpixels"
  - "noise"
  - "perlin-noise"
  - "pixels"
  - "texture"
  - "updatepixels"
coverImage: "Perlin_Noise_Texture.png"
---

Nei [due](https://blog.federicopepe.com/2016/06/random-vs-perlin-noise/) [post](https://blog.federicopepe.com/2016/07/altri-esempi-con-la-funzione-noise/) precedenti abbiamo sempre usato la funzione _noise()_ in modo mono dimensionale. È arrivato il momento di fare un passo in avanti e aggiungere la seconda dimensione.

## Ripasso: 1D Perlin Noise

Quando parliamo di Perlin Noise mono dimensionale dobbiamo immaginare i valori su una linea temporale orizzontale; quando noi chiediamo alla funzione di restituirci un determinato valore di noise, tale valore sarà correlato a quello precedente e a quello successivo. Nell'immagine viene rappresentato il valore di noise con parametro xOff pari a 3.32. Come nel [post precedente](https://blog.federicopepe.com/2016/07/altri-esempi-con-la-funzione-noise/), l'incremento che ho usato per generare l'immagine è 0.02.

[![Perlin Noise Monodimensionale](/assets/images/1D_Perlin_Noise-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/07/1D_Perlin_Noise.png)

## 2D Perlin Noise

Quando aggiungiamo una dimensione, invece, dobbiamo pensare a una griglia i cui valori sono correlati tra loro sia sull'asse delle x che su quello delle y.

[![2D Perlin Noise](/assets/images/2D_Perlin_Noise_Grid-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/07/2D_Perlin_Noise_Grid.png)

Come si evince dall'immagine, la situazione diventa più complicata perché se analizziamo singolarmente i punti centrali rosso o blu intuiamo facilmente la correlazione con i punti che li circondano. Se li consideriamo entrambi contemporaneamente, invece, notiamo subito come ci siano dei punti in comune che dovranno essere a loro volta correlati tra loro.

Questo è un esempio molto semplificato: provate a immaginare se ciascuno dei punti disegnati fosse un pixel!

## Generiamo una texture

È arrivato il momento di sporcarsi le mani e scrivere un po' di codice: lo scopo del programma di oggi è generare una texture con Processing utilizzando Perlin Noise bidimensionale.

Partiamo da un'analisi del risultato finale per capire tutti i passaggi e il codice che ci serve:

[![Texture generata con Perlin Noise bidimensionale](/assets/images/Perlin_Noise_Texture-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/07/Perlin_Noise_Texture.png)

Per generare la texture dobbiamo prendere ciascun pixel della nostra finestra facendo in modo che il suo colore sia correlato ai pixel vicini: è facile notare come ci siano delle aree più scure e altre più chiare e che, in generale, la texture generata sia uniforme.

Per farvi capire la differenza, nell'immagine qui sotto ho sostituito nel programma la funzione _noise()_ con _random():_

[![Random Texture Processing](/assets/images/Processing_Random_Texture-1-988x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2016/07/Processing_Random_Texture-1.png)

Sostituendo la funzione noise() con random() il risultato è molto differente.

Per lavorare con i pixel utilizzeremo le funzioni _**[loadPixels()](https://processing.org/reference/loadPixels_.html)**_ e **_[updatePixels()](https://processing.org/reference/updatePixels_.html)_** che avremo modo di analizzare in modo approfondito in futuro. Per il momento vi basti sapere che la prima funzione carica tutti i pixel della finestra in un array chiamato **_pixels\[\]_** e che la seconda ricarica i pixel nella finestra dopo che sono stati modificati.

Un altro punto molto importante è sapere che, benché i pixel presenti in una finestra siano un insieme di righe e colonne, nell'array pixels\[\] vengono salvati con numero progressivo.

Per modificare il colore di ciascun pixel della finestra abbiamo bisogno di due cicli [for annidati](https://blog.federicopepe.com/2015/11/loop-for-e-nesting/): uno per i valori di x, l'altro per quelli di y. La funzione **_noise()_** entra in gioco proprio in questa fase: attraverso due variabili – _**xOff**_ e **_yOff_** – imposteremo il colore di ciascun pixel.

Ecco il codice finale:

```
/*
 * Texture con Perlin Noise 2D
 * by Federico Pepe
 *
 */

float increment = 0.015;

void setup() {
  size(500, 500);
}

void draw() {
  // Carico i pixel della finestra
  loadPixels();
  float xOff = 0;
  for(int x = 0; x < width; x++) {
    xOff += increment;
    float yOff = 0;
    for (int y = 0; y < height; y++) {
      yOff += increment;
      // Ottengo il valore noise passando le variabili xOff e yOff.
      float bright = noise(xOff, yOff) * 255;
      // Riassegno a ogni pixel il nuovo colore
      pixels[x+y*width] = color(bright);
    }
  }
  // Aggiorno tutti i pixel della finestra
  updatePixels();
}
```

Domanda: perché non ho inizializzato le due variabili xOff e yOff all'inizio del programma? Cosa succede se non reimposto a 0 la variabile yOff a ogni ciclo?

Per aggiungere l'interazione con l'utente, aggiungiamo subito dopo _updatePixels()_ la seguente riga: `increment = map(mouseX, 0, width, 0.1, 0.01);`

In questo modo rimapperemo la posizione X del mouse che può andare da 0 alla larghezza della finestra in un nuovo range compreso tra 0.1 e 0.01.
