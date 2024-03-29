---
title: "Glitch di un'immagine con Processing"
date: "2017-09-23"
categories: 
  - "processing-images"
tags: 
  - "brightness"
  - "glitch"
  - "glitch-art"
  - "saturation"
coverImage: "Glitch-immagine-export.png"
---

## Breve introduzione alla Glitch Art

Per **Glitch Art** intendiamo la pratica sfruttare e/o introdurre in un'opera degli errori analogici o digitali per fini estetici. Nel mondo dell'analogico si interviene direttamente sugli apparecchi elettronici che registrano o riproducono l'opera. Per quanto riguarda il digitale, invece, tale manipolazione è resa ancora più semplice dagli strumenti tecnologici di cui disponiamo che ci consentono di accedere direttamente ai dati e di farne ciò che vogliamo. Questa pratica è anche chiamata _databending._

Non si tratta di un movimento artistico nato, come si potrebbe pensare, negli ultimi anni con la democratizzazione della tecnologia e degli strumenti creativi ma, al contrario, affonda le sue radici nella prima metà del novecento: il filmato qui sotto _A Colour Box_ dell'artista neo-zelandese _Len Lye_ e datato 1935 è considerato uno dei primi esempi di glitch art.

https://www.youtube.com/watch?v=q-4k3A-ZHqM

Benché negli ultimi anni abbia riscosso un sempre maggiore successo, questo movimento artistico non è mai diventato mainstream. Possiamo sfruttare quello che abbiamo imparato a fare con Processing per fare i nostri esperimenti di glitch art e per studiare qualche nuova funzione del linguaggio.

## Usiamo Processing per creare un effetto glitch

Lo scopo di oggi è prendere una foto e _glitcharla_. Nell'esempio proposto non andrò a introdurre un vero e proprio errore nell'immagine ma andrò a manipolare direttamente l'array di pixel per ricreare un effetto artistico simil-glitch. Il motivo è presto detto: per ottenere un effetto artistico godibile è meglio evitare di usare variabile non controllabili.

\[caption id="attachment\_1260" align="aligncenter" width="640"\]![Glitch fotografia Processing](/assets/images/Glitch-Immagine-Processing.jpg) Immagine di partenza\[/caption\]

L'immagine di partenza non è stata scelta in modo casuale: dal momento che useremo la funzione _brightness(),_ che restituisce il valore della luminosità di un colore, la foto presenta un forte contrasto tra lo sfondo e le sagome nere e la parte centrale illuminata dalle fiamme.

```java
/*
 * Glitch di un'immagine con Processing
 * Federico Pepe, 23.09.2017
 * http://blog.federicopepe.com/processing
 */

PImage img;
int minThreshold = 200;
int maxThreshold = 255;

void setup() {
  size(1, 1);
  surface.setResizable(true);
  img = loadImage("fire.jpg");
  surface.setSize(img.width, img.height);  

  noStroke();
  noLoop();
}

void draw() {
  background(255);
  image(img, 0, 0);
  img.loadPixels();

  for (int y = 0; y < height; y++) {
    for (int x = 0; x < width; x++) {

      if (brightness(img.pixels[y*width+x]) > minThreshold && brightness(img.pixels[y*width+x]) < maxThreshold) {
        color c = get(x, y);
        stroke(c);
        line(x, y, x, y+2);
        noFill();
      }
    }
  }
}

void mousePressed() {
  save("export/export.png");
}
```

Rispetto al codice visto negli ultimi post, ho aggiunto due variabili di soglia **minTreshold** e **maxThreshold** e, all'interno del classico ciclo for che va ad analizzare ogni singolo pixel dell'immagine, introdotto un semplice controllo condizionale che, qualora il risultato sua _true_ disegna una linea verticale di 2 pixel dello stesso colore del pixel analizzato.

![Glitch immagine esportata](/assets/images/Glitch-immagine-export.png)

Il risultato è sicuramente particolare e d'effetto. Potete provare a giocare un po' con i parametri di soglia oppure sostituendo il disegno della linea con un quadrato. Un'altra possibilità potrebbe essere quella di non utilizzare il parametro della _luminosità_ ma andare a scegliere la [saturazione](https://processing.org/reference/saturation_.html) o il [colore](https://processing.org/reference/color_.html) stesso.

\[caption id="attachment\_1263" align="aligncenter" width="640"\]![Glitch with squares](/assets/images/Glitch-with-square.png) Lo stesso identico codice di prima ma, in questo esempio, ho sostituito line() con rect()\[/caption\]
