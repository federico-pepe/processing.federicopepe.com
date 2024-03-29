---
title: "Il problema dei grafici a linee curve"
date: "2019-08-15"
categories: 
  - "data"
tags: 
  - "beziervertex"
  - "curvevertex"
  - "data-visualization"
  - "grafico-a-linee"
  - "infografiche"
coverImage: "grafico-a-linee-curve-errore-curvatura.jpg"
---

Dopo aver realizzato il nostro [grafico a linee](https://blog.federicopepe.com/2018/05/grafico-a-linee/), potremmo pensare di utilizzare delle linee curve. Ma, come vedremo in questo articolo, ci troveremo ad affrontare una serie di problemi.

## Dalle linee dritte a linee curve

Ripartendo dal codice nell'articolo precedente e cambiato le seguenti righe:

```
vertex(x1, height - 50 + tempMin[i] * - 20);
```

```
vertex(x1, height - 50 + tempMax[i] * - 20);
```

utilizzando **curveVertex()** al posto di **vertex()** otteniamo questo risultato:

[![grafico linee curve utilizzando curveVertex](images/grafici-a-barre-curveVertex-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2019/08/grafici-a-barre-curveVertex.jpg)

Notiamo subito che mancano dei collegamenti con il primo e l'ultimo punto della serie di dati. Come indicato nel [reference](https://www.processing.org/reference/curveVertex_.html), questa funzione utilizza il primo e l'ultimo punto vengono usati per guidare la curvatura della linea.

A questo punto dobbiamo _arbitrariamente_ aggiungere due punti e, in questo caso, conviene farlo prima e dopo il ciclo for. Qui sorge il secondo problema: che coordinate diamo a questi due punti che non derivano dal nostro dataset?

La soluzione più ovvia è utilizzare le coordinate del primo e dell'ultimo punto:

```java
// Temperature minime
  int x1 = 68;
  beginShape();
  curveVertex(x1, height - 50 + tempMin[0] * - 20); 
  for (int i = 0; i < tempMin.length; i++) {
    fill(100, 190, 255);
    curveVertex(x1, height - 50 + tempMin[i] * - 20);
    noStroke();
    ellipse(x1, height - 50 + tempMin[i] * - 20, 10, 10);
    x1 += 40;
    stroke(100, 190, 255);
    noFill();
  }
  curveVertex(x1, height - 50 + tempMin[tempMin.length - 1] * - 20); 
  endShape();

  // Temperature massime
  x1 = 68;
  beginShape();
  curveVertex(x1, height - 50 + tempMax[0] * - 20); 
  for (int i = 0; i < tempMax.length; i++) {
    fill(255, 100, 100);
    curveVertex(x1, height - 50 + tempMax[i] * - 20);
    noStroke();
    ellipse(x1, height - 50 + tempMax[i] * - 20, 10, 10);
    x1 += 40;
    stroke(255, 100, 100);
    noFill();
  }
  curveVertex(x1, height - 50 + tempMax[tempMax.length - 1] * - 20); 
  endShape();
```

Se lanciamo il programma, il nostro grafico a linee curve diventa così:

[![Grafico a linee curve in Processing](images/grafici-a-linee-curve-Processing-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2019/08/grafici-a-linee-curve-Processing.jpg)

Il risultato potrebbe sembrare soddisfacente ma un occhio esperto si potrebbe accorgere di un altro problema: la curvatura delle linee intorno ai punti dei dati può confonderci e portarci in errore quando leggiamo il grafico.

## L'errore di precisione

Questo set di dati ha dei data point molto vicini tra loro e, quindi, il fenomeno non si vede chiaramente.

Ho realizzato quest'altra immagine per mostrarlo meglio: questa volta i punti sono inseriti in un array in modo casuale ma il principio è lo stesso di quello utilizzato nello sketch che stiamo realizzando.

[![Grafico a linee curve con errore](images/grafico-a-linee-curve-errore-curvatura-988x1024.jpg)](https://blog.federicopepe.com/wp-content/uploads/2019/08/grafico-a-linee-curve-errore-curvatura.jpg)

È evidente l'errore che esiste tra i primi due punti e gli ultimi due: la linea curva va oltre i valori in modo anomalo e portando a un'interpretazione errata del grafico.

Come trovare la soluzione definita al nostro problema? Abbiamo due possibilità:

1. Rinunciare alle linee curve una volta per tutte
2. Non usare la funzione _curveVertex()_ ma usare le curve di Bézier e, quindi, la funzione **[bezierVertex()](https://processing.org/reference/bezierVertex_.html)**.

La difficoltà dell'usare queste curve è di dover passare alla funzione tre coordinate x e y: due per i punti di controllo e una per il punto di ancoraggio. Se volete capire come funzionano, consiglio di provare a giocare al [The Bézier Game](https://bezier.method.ac) (io ho rinunciato dopo poco).
