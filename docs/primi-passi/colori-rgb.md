# Colori RGB

Nell'ultimo post abbiamo imparato cosa sono le [primitive 2D](https://blog.federicopepe.com/2015/07/primitive-2d-point-line-rect-ellipse-triangle/) e siamo riusciti a far disegnare al nostro computer alcune semplici forme geometriche sullo schermo. Nel realizzare questi semplici sketch forse qualcuno di voi avrà notato una particolarità: di default Processing colora di bianco l'interno della forma e di nero il bordo mentre lo sfondo dello sketch rimane grigio.

![Processing's function ellipse()](/assets/images/sketch_150728e_Processing_ellipse-988x1024.png)

## RGB: Red, Green and Blue

Prima di cominciare a utilizzare i colori è importante capire come funzionano. Alle scuole elementari si impara che attraverso la miscelazione dei tre colori primari, **rosso**, **giallo** e **blu**, si possono ottenere tutti i colori nelle diverse sfumature. Anche gli schermi funzionano in modo simile ma i tre colori di base sono **rosso**, **verde** e **blu** in inglese **RGB**.

![Colori RGB](/assets/images/RGB_Color.png)

Grazie a questa immagine si può capire come ottenere i colori secondari:

- rosso + verde = giallo
- rosso + blu = viola
- verde + blu = azzurro
- rosso + verde + blu = bianco
- nessun colore = nero

## Le funzioni fill() e stroke()

In Processing esistono due funzioni per colorare le forme: _fill()_ e _stroke()_. Con la prima indichiamo il colore di _riempimento_ della forma mentre, con la seconda, il colore del bordo.

Quando lavoriamo nella modalità RGB, che è quella di default, queste due funzioni possono accettare _uno_, _due_, _tre_ o _quattro parametri_.

Facciamo degli esempi pratici:

### Utilizzo di tre parametri per assegnare un colore

```java
size(500, 500);
fill(255, 0, 0);
ellipse(250, 250, 150, 150);
```

![Cerchio Rosso](/assets/images/Processing_RGB_CerchioRosso-988x1024.png)

Se provo a tradurre in italiano quanto scritto nel codice, le istruzioni date al computer sarebbero:

- Disegna una finestra di 500 pixel di larghezza e 500 pixel di altezza.
- Colora la forma con la massima quantità di rosso (255), niente verde (0), e niente blu (0).
- Disegna un ellisse con centro nella posizione x = 250, y = 250, larghezza = 150 e altezza = 150.

Non avendo specificato un parametro per il colore del bordo, come accaduto in precedenza, Processing utilizzerà il parametro di default e colorerà il bordo di nero.

Ora facciamo una piccola modifica e aggiungiamo una riga al nostro codice:

```java
size(500, 500);
fill(255, 0, 0);
stroke(0, 0, 255);
ellipse(250, 250, 150, 150);
```

Ora abbiamo aggiunto la funzione _stroke()_ assegnando i parametri rosso = 0, verde = 0, blu = 255 e questo è il risultato:

![Cerchio rosso con bordo blu](/assets/images/Processing_RGB_CerchioRossoBordoBlu-988x1024.png)

Come avrete capito, se utilizzo tre parametri nelle funzioni _fill()_ e _stroke()_ sto indicando la quantità di rosso, verde e blu il cui valore deve essere compreso tra 0, il valore minimo, e 255, quello massimo.

### Un parametro solo: la scala di grigi

Come scritto in precedenza, entrambe le funzioni possono accettare anche un solo parametro: in questo caso Processing considererà il valore inserito come valore assegnato a tutti e tre i parametri RGB.

Scrivere:

```fill(127):```

Equivale a:

```fill(127, 127, 127);```

Facendo un po' di esperimenti con i colori, scoprirete che quando i parametri RGB sono equivalenti, sto lavorando in scala di grigi.

Per ottenere il bianco, infatti, mi basterà scrivere: **fill(255)** mentre, per il nero **fill(0)**.

### Due o quattro parametri: la trasparenza

Se utilizziamo due parametri con il primo indichiamo il colore nella scala di grigi che abbiamo scelto e con il secondo impostiamo un livello di trasparenza in una scala da 0 (completamente trasparente) a 255 (completamente opaco).

Quando, invece, utilizziamo quattro parametri stiamo aggiungendo la trasparenza a un colore specifico dettato dai primi tre parametri.

```java
size(500, 500);
fill(255, 0, 0, 100);
stroke(0, 0, 255);
ellipse(250, 250, 150, 150);
```

![RGB with Transparency](/assets/images/Processing_RGB_Transparency-988x1024.png)

## background(), noFill() e noStroke()

Finora abbiamo sempre parlato di colorare forme. Ma se volessimo modificare lo sfondo della finestra dobbiamo ricorrere alla funzione _background()_ che, per quanto concerne la sintassi e il numero di parametri accettati dalla funzione, ricalca fill() e stroke().

```java
background(0);
size(500, 500);
fill(255, 0, 0, 100);
stroke(0, 0, 255);
ellipse(250, 250, 150, 150);
```

![background(0)](/assets/images/Processing_background-988x1024.png)

Con le funzioni _noFill()_ e _noStroke()_ – attenzione alle maiuscole! – possiamo eliminare il colore del bordo o quello di riempimento. Com'è facile intuire, queste funzioni non richiedono alcun parametro.

## Color selector

Giustamente vi starete chiedendo: come faccio a conoscere i valori RGB di un determinato colore? Non vi preoccupate, Processing mette a disposizione uno strumento molto utile chiamato **Color Selector** accessibile dal menu _Tools > Color Selector_ la cui funzione è esattamente quella di aiutarvi nella selezione dei colori.

![Color Selector](/assets/images/Processing_Color_Selector.png)

Oltre ai valori RGB, troviamo anche quelli HSB e Hexadecimal di cui parleremo prossimamente.

## Mettiamo tutto insieme

### Esempio 1:

```java
/*
 *  Colori RGB
 *  Federico Pepe
 *  http://blog.federicopepe.com/processing
 */
 
// Impostiamo la dimensione della finestra a 500x500px
size(500, 500);
// Impostiamo lo sfondo di colore bianco
background(255);
// Impostiamo di non avere un bordo
noStroke();
// Impostiamo una tonalità di rosso come riempimento
fill(255, 157, 157);
// Disegnamo il primo cerchio
ellipse(100, 250, 100, 100);
// Impostiamo il bordo di colore nero
stroke(0);
// Disegniamo il secondo cerchio
ellipse(250, 250, 100, 100);
// Impostiamo una tonalità di verde come riempimento
fill(157, 255, 179);
// Disegniamo il terzo cerchio
ellipse(400, 250, 100, 100);
```

Sono tante linee di codice ma non spaventatevi! Prima di analizzare il risultato vorrei introdurre un'ultima novità: l'utilizzo dei commenti nel codice.

I programmatori spesso commentano il proprio codice per spiegare brevemente come funziona quella porzione di codice oppure per lasciare dei promemoria o delle indicazioni. I commenti sono utili sia se dobbiamo condividere il nostro codice con altre persone sia per ricordare a noi stessi come funzionava quel particolare programma.

Quando diventerete dei programmatori esperti, sarà interessare recuperare dall'hard disk i vostri primi programmi e confrontarli con gli ultimi. È per questo che io ho preso l'abitudine di inserire sempre, all'inizio di ogni programma, la data di creazione o di ultima modifica.

Se dovete scrivere un commento di molte righe di testo come, ad esempio, l'intestazione all'inizio del programma, dovete utilizzare **/\*** per indicare l'inizio del commento e **\*/** per indicarne la fine.

Se, invece, il commento è di una sola riga, è sufficiente scrivere **//** all'inizio della riga stessa.

Il codice qui sopra darà questo risultato:

![Processing RGB Color Example 1](/assets/images/Processing_RGB_ColorExample1-988x1024.png)

La cosa interessante da notare è che una volta specificato un colore con la funzione _fill()_ o _stroke()_, rimarrà impostato anche per le forme successive finché non utilizziamo la funzione _noFill()_ o _noStroke()_ oppure finché non impostiamo nuovamente il colore.

Nello sketch di esempio, infatti, il riempimento di colore rosso viene settato solo una volta all'inizio eppure viene applicato ai primi due cerchi così come il bordo nero, inserito subito prima di disegnare la seconda forma, rimane anche per la terza.

### Esempio 2

```java
/*
 *  Colori RGB e trasparenza
 *  Federico Pepe
 *  http://blog.federicopepe.com/processing
 */
 
// Impostiamo la dimensione della finestra a 500x500px
size(500, 500);
// Impostiamo lo sfondo di colore nero
background(0);
// Impostiamo di non avere un bordo
noStroke();
// Impostiamo una tonalità di rosso come riempimento
fill(255, 0, 0, 127);
// Disegnamo il primo cerchio
ellipse(200, 250, 150, 150);
// Disegniamo il secondo cerchio
ellipse(250, 250, 150, 150);
// Impostiamo una tonalità di verde come riempimento
fill(127, 255, 127);
// Disegniamo il terzo cerchio
ellipse(300, 250, 150, 150);
```

![Esempio 2](/assets/images/Processing_RGB_ColorExample2-988x1024.png)

In questo secondo esempio ho utilizzato la trasparenza nei primi due cerchi rossi (notate cosa succede quando si sovrappongono). Il terzo cerchio, quello verde, non avendo un parametro per la trasparenza ed essendo l'ultimo inserito nello sketch viene disegnato "sopra" gli altri due.

## Compiti per casa

Arrivati a questo punto, è il momento di mettersi in gioco. Imparare a programmare non significa soltanto studiare, capire la sintassi e copiare-incollare del codice trovato su internet ma anche porsi dei problemi e provare a risolverli autonomamente.

Ho pensato che per rendere questa serie di post più interessante fosse necessario introdurre dei _compiti a casa_ per dare la possibilità, a voi che leggete, di sbattere un po' la testa.

Il compito di questa settimana è realizzare uno sketch ispirato alle composizioni geometriche di [**Piet Mondrian**](https://www.google.it/search?q=mondrian&hl=it&biw=1256&bih=742&site=webhp&source=lnms&tbm=isch&sa=X&sqi=2). Potete inviare le vostre soluzioni nei commenti qui sotto oppure via twitter [@fedpep](http://www.twitter.com/fedpep).
