# Introduzione agli oggetti

È finalmente arrivato il momento di cominciare a parlare di **programmazione orientata agli oggetti** ma, prima di addentrarci nel codice e modificare i nostri sketch, è importante dare una definizione chiara e semplice di che cosa sono gli oggetti e di come li possiamo utilizzare.

Questo post, quindi, non conterrà esempi pratici ma fornirà un'introduzione generale all'argomento. Ho deciso di muovermi in questo modo perché quando mi sono trovato ad affrontare per la prima volta l'OOP ho faticato a capire il reale vantaggio di un approccio ad oggetti. Oggi invece, non potrei farne a meno.

Partiamo con una buona notizia: per utilizzare gli oggetti non dobbiamo imparare nulla di nuovo rispetto a quanto fatto fino ad ora. Utilizzeremo [variabili](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/), [controlli condizionali](https://blog.federicopepe.com/2015/09/controlli-condizionali-if-else-if-else/), [loop](https://blog.federicopepe.com/2015/11/loop-while/) e [funzioni](https://blog.federicopepe.com/2015/11/funzioni-personalizzate/). Se siete arrivati a questo punto e avete ancora dei dubbi in merito anche solo ad uno di questi argomenti, il mio consiglio è di fermarsi ora e andare a rileggere i vecchi post. Se, invece, è tutto chiaro, procediamo!

## Oggetti: questione di astrazione

Nella realtà di tutti i giorni siamo abituati ad avere a che fare con oggetti specifici ciascuno con caratteristiche peculiari che dipendono, in gran parte, dalla marca e dal modello che possediamo. Questi oggetti, però, possono essere astratti a un livello più alto: pensiamo, ad esempio a una macchina.

Se potessi leggere nelle vostre menti, vedrei che ciascuno di voi sta pensando a una macchina differente dagli altri ma che, in quanto oggetto-macchina, ha delle caratteristiche comuni a tutte le altre: ad esempio il numero di ruote sarà uguale per tutti mentre il colore della carrozzeria sarà differente.

È importante notare come l'oggetto-macchina possa avere dei _dati_ (colore, lunghezza, numero porte, ...) e delle _funzioni_ (si muove in avanti, si muove indietro, ...).

Facciamo un passo in più: l'astrazione della macchina non rappresenta di per sé una macchina vera e propria. Il modello-macchina astratto funge da _template._ In programmazione, l'oggetto astratto viene chiamato _classe_. Ciascuna macchina che prenderà come base il modello astratto ma avrà caratteristiche peculiari sarà a tutti gli effetti un _oggetto_ vero e proprio. In programmazione, quando richiamiamo la classe per costruire un nuovo oggetto stiamo creando un'_istanza della classe_.

## Ricapitolando

Abbiamo un modello astratto che fungerà da _«template»_ per tutti gli oggetti che andremo a creare che chiamiamo _classe_ mentre creando un'_istanza_ della classe creiamo effettivamente un _oggetto_.

## Cosa c'è di nuovo?

Fino a qui tutto ok, ma qual è la vera novità? Le variabili legate agli oggetti, così come le funzioni legate alle azioni che questi oggetti devono compiere all'interno del nostro programma, saranno all'_interno della classe_.

Con la programmazione a oggetti il codice si semplificherà ulteriormente perché non andremo a «sporcare» il codice con informazioni inutili. Ci basterà richiamare la classe perché ciascun oggetto avrà tutto quello di cui necessita al suo interno.

Nel prossimo post vedremo la sintassi corretta da utilizzare sia delle classi che degli oggetti e poi, finalmente, cominceremo a sporcarci un po' le mani.
