---
title: "Schermo, pixel e linee"
date: "2015-07-22"
---

Una volta scaricato e installato Processing, è arrivato il momento di cominciare sporcarsi le mani e a programmare il nostro primo _sketch_. Se apriamo l'IDE e clicchiamo sul pulsante _Run_ senza scrivere alcuna riga di codice, dopo qualche secondo comparirà una finestra simile a quella nell'immagine qui sotto.

![Il nostro primo sketch in Processing.](/assets/img/Processing_primo_sketch-275x300.png)

Complimenti! Questo è il vostro primo programma _funzionante_ realizzato con questo linguaggio di programmazione. Mi rendo conto che per molti, a prima vista, potrebbe non sembrare una grande conquista ma vi assicuro che se avessimo dovuto raggiungere lo stesso risultato con altri linguaggi, non sarebbe stato così semplice.

## Lavorare con i pixel

Lo schermo è la nostra tela. Prima di cominciare a disegnare qualcosa su di esso è dunque necessario fare un paio di considerazioni a riguardo: per prima cosa lo schermo è composto da una **griglia di pixel** che, per semplicità, possiamo paragonare a un foglio di carta millimetrata.

Il pixel è dunque la nostra **unità di misura** e la sua dimensione è così ridotta che, a occhio nudo, è difficile distinguere un pixel da quello adiacente.

Quando alle elementari abbiamo cominciato a disegnare punti, linee e forme geometriche sulla carta millimetrata, siamo stati abituati a lavorare all'interno di un **piano cartesiano** con punto di origine (0, 0) normalmente posizionato al centro del foglio come nell'immagine seguente.

![Un piano cartesiano "tradizionale".](/assets/img/Processing_piano_cartesiano.png)

La differenza principale rispetto a come siamo sempre stati abituati a ragionare è che sullo schermo del computer il punto di origine non si trova al centro ma nell'angolo in alto a sinistra.

![Coordinate Schermo](/assets/img/Processing_piano_schermo.png)

Come è facile intuire, il vantaggio di questo sistema è che qualsiasi punto sullo schermo ha sempre un valore positivo; questo ci tornerà molto utile quando cominceremo a fare dei programmi più complessi.

## Disegnamo una linea sullo schermo

Copiate e incollate questo codice su Processing e poi premete il tasto _Run_.

```java
size(500, 500);
line(100, 150, 400, 250);
```

Questo è il risultato che dovrebbe comparirvi: una linea nera su sfondo grigio.

![La nostra prima linea.](/assets/img/Processing_line-988x1024.png)

Nel caso in cui questo non avvenga, è possibile che abbiate sbagliato qualcosa nel copia-incolla. Provate a cliccare su _view raw_ e ricopiare nuovamente le due linee di codice.

Per questo _sketch_ abbiamo utilizzato due linee di codice con due **funzioni**: [size()](https://processing.org/reference/size_.html) e [line()](https://processing.org/reference/line_.html). Se andiamo a cercare nel Reference, il manuale sul sito di Processing, scopriamo a cosa servono e qual è la sintassi corretta da utilizzare: _size(width, height)_ serve per determinare la grandezza della finestra su cui vogliamo lavorare e accetta due parametri: larghezza (in inglese width) e altezza (in inglese height); _line(x1, y1, x2, y2)_, invece, disegna una linea sullo schermo e, per funzionare, ha bisogno di quattro parametri: le coordinate x e y del punto di partenza e di arrivo.

In buona sostanza abbiamo scritto un programma con le seguenti istruzioni:

1. Disegna una finestra di 500 pixel di altezza e 500 pixel di larghezza.
2. Disegna una linea dal punto con coordinata x = 100 e y = 150 al punto con coordinate x = 450, y = 250.

Non abbiamo dato nessun'altra indicazione e Processing ha utilizzato dei **valori di default** per tutto il resto: il grigio dello sfondo e il nero della linea.

## L'importanza del punto e virgola

Un'ultima cosa da notare è che, a differenza di quando scriviamo, in programmazione utilizziamo il **punto e virgola** per separare le varie istruzioni anziché il punto fermo. Questa è una cosa da memorizzare e imparare subito: molto spesso, i nostri programmi non funzionano perché ci siamo dimenticati di mettere proprio un punto e virgola al termine di un'istruzione (nei prossimi post vi insegnerò come riconoscere questo genere di errori grazie al debugger). A differenza di noi umani che non abbiamo problemi a leggere un testo anche se manca un punto, i computer non riescono capire se un'istruzione è finita in assenza del punto e virgola.
