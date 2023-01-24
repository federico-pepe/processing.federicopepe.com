# Controlli condizionali: if, else if, else

Abbandoniamo temporaneamente la casualità generata dalla funzione [random(), che abbiamo visto la scorsa settimana](/primi-passi/println-e-random/), per immergerci nel mondo dei _controlli condizionali._

Nella vita di tutti i giorni siamo condizionati da scelte: siamo abituati a pensare che _**se**_ facciamo qualcosa _**allora**_ accadrà qualcosa di specifico **_altrimenti_** (cioè nel caso in cui non si verifichi la condizione iniziale), non succederà nulla.

Il nostro obiettivo di oggi è avere la possibilità di creare una logica simile all'interno dei nostri programmi ovvero far eseguire determinate parti di codice solo al verificarsi di condizioni specifiche. Stiamo cercando di fare qualcosa di simile a quello che abbiamo [già visto con mousePressed() e keyPressed()](/primi-passi/eventi-mousepressed-e-keypressed/) ma, questa volta, vogliamo avere ancora più controllo.

## Espressioni e variabili booleane

I computer, purtroppo (o per fortuna), non sono macchine intelligenti e seguono una logica abbastanza semplice: una condizione può essere _vera_ oppure _falsa_, in inglese _true_ o _false_. Nell'elenco dei [tipi di variabili](/primi-passi/variabili-in-processing-creazione-e-personalizzazione/) più comuni ho volutamente escluso quelle di tipo booleano: variabili, dunque, che possiamo creare e inizializzare e a cui possiamo assegnare solo uno di questi due valori.

Una cosa molto importante è che non può esistere in nessun programma una variabile che sia contemporaneamente _vera_ e _falsa._

### Operatori di confronto

Dal momento che ci troveremo spesso a lavorare con dei valori numerici, possiamo utilizzare gli operatori di confronto/comparazione:

- Maggiore: >
- Minore: <
- Maggiore o uguale: >=
- Minore o uguale: <=
- Uguale: ==
- Diverso: !=

## Controlli condizionali

Per inserire un controllo condizionale è sufficiente tradurre in inglese le parole che ho sottolineato precedentemente e creare dei blocchi di codice con le classiche parentesi graffe: il _se_ diventa, dunque, **if** mentre l'_altrimenti_ si traduce con **else**.

```java
if(condizione) {
 /* La porzione di codice qui inserita verrà eseguita
 * esclusivamente se la condizione sopra indicata
 * sarà true, quindi vera.
 */
} else {
 /* Nel caso in cui la condizione sopra inserita NON
 * sia vera, verrà eseguita questa porzione di codice
 */
}
```

Nel campo _condizione_ dobbiamo inserire la nostra espressione di controllo.

### Esempio 1:

```java
/*
 * Controlli condizionali: if, else if, else
 * by Federico Pepe
 * http://blog.federicopepe.com
*/
void setup() {
  size(500, 500);
  stroke(255);
}
void draw() {
  if(mouseX > width/2) {
    background(0);
  } else {
    background(127);
  }
  line(width/2, 0, width/2, height); 
}
```

Con questo programma verifichiamo se la posizione X del mouse è **maggiore** della metà della larghezza. In caso positivo (true), lo sfondo della finestra verrà colorato di nero, in caso contrario (false) di un grigio scuro.

Per comodità ho creato una linea bianca che mi segnala esattamente il punto da oltrepassare per vedere lo sfondo cambiare colore. Avendo utilizzato la condizione maggiore se il valore di mouse X è pari a 250, la metà della larghezza, la condizione sarà ancora considerata _false_.

### Esempio 2:

![Esempio if 1](/assets/images/esempio_if_processing_1.png){ width="30%" }
![Esempio if 2](/assets/images/esempio_if_processing_2.png){ width="30%" }
![Esempio if 3](/assets/images/esempio_if_processing_3.png){ width="30%" }

```java
/*
 * Controlli condizionali: if, else if, else
 * by Federico Pepe
 * http://blog.federicopepe.com
 */
void setup() {
  size(500, 500);
  stroke(255);
}
void draw() {
  if (mouseX > 200) {
    background(200);
  } else if (mouseX > 100) {
    background(127);
  } else {
    background(0);
  }
  line(100, 0, 100, height);
  line(200, 0, 200, height);
}
```

In questo secondo esempio abbiamo due condizioni differenti: _se_ la X del mouse è maggiore di 200 lo sfondo sarà grigio chiaro, _altrimenti se_ (**else if**) è maggiore di 100 lo sfondo sarà grigio scuro, altrimenti sarà nero. È possibile concatenare molteplici condizioni else if per coprire tutti i casi che ci interessa verificare.

La prossima settimana faremo altri esempi per essere sicuri di aver appreso il funzionamento dei controlli condizionali; nel frattempo sbizzarritevi con i vostri sketch.
