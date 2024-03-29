---
title: "Caricare file esterni in Processing"
date: "2016-12-20"
categories: 
  - "processing"
tags: 
  - "file"
  - "immagini"
  - "jpg"
  - "media"
coverImage: "Processing_Data_Folder.png"
---

In tutti gli esempi visti finora abbiamo sempre utilizzato le funzioni interne di Processing per disegnare qualcosa sullo schermo. È possibile, ovviamente, caricare all'interno dei nostri sketch file esterni in vari formati come, ad esempio, font, immagini, file vettoriali, suoni e altro.

Dati gli argomenti che affronteremo a breve, è importante capire come effettuare questa operazione nel modo corretto per evitare di incorrere in problemi soprattutto quando distribuiamo i nostri programmi ad altre persone.

**La prima regola fondamentale** che dobbiamo sempre tenere a mente è che prima di poter essere utilizzati, i file devono essere caricati dal nostro sketch. Questo avviene **ogni volta** che lanciamo il programma.

Processing è in grado di caricare file che:

- si trovano all'interno della cartella dello sketch
- si trovano in una cartella qualsiasi sul computer
- si trovano su un server accessibile via internet.

Ciascuna di queste situazioni presenta dei pro e dei contro e non esiste una soluzione che possa andare bene in tutti i casi. La prima opzione è, però, quella più comune.

[![Caricare file esterni in Processing](/assets/images/Processing_Data_Folder-1024x636.png)](https://blog.federicopepe.com/wp-content/uploads/2016/12/Processing_Data_Folder.png)

Tutti i file esterni sono generalmente inseriti in una cartella chiamata _data_ che troviamo all'interno della cartella dello sketch.

## Aggiungere file dal menu

Cliccando sul menu _Sketch > Add File..._ si aprirà una finestra di dialogo dove andremo a selezionare il file da inserire.

![](/assets/images/Processing-add-data-from-menu-1.gif)

## Drag and drop

La seconda opzione, forse la più comoda, permette di trascinare uno o più file direttamente nella finestra di processing.

![Processing drag and drop](/assets/images/Processing-add-media-drag-drop.gif)

## Aggiunta manuale

Oppure è possibile aggiungere i file manualmente aprendo la cartella dello sketch dal menu _Sketch > Show Sketch Folder_, scorciatoia ⌘+K, creando una cartella _data_ (se non esiste) e copiando direttamente i file all'interno di essa.

![Processing aggiungere file manualmente](/assets/images/processing-add-media-manually.gif)

## Consigli

Quando andremo a caricare il o i file è buona regola specificare l'estensione, ad esempio **"file.txt"** e fare attenzione all'uso delle lettere maiuscole: se il file si chiama _immagine.jpg_ provare a caricare _Immagine.jpg_, _immAgine.jpg_ o _immagine.JPG_ genererà sempre un errore.

Per rendere il contenuto del file disponibile all'interno dell'interno programma, normalmente si crea una variabile globale al di fuori dei cicli di _setup()_ e _draw()_ come avevo spiegato [qui nel paragrafo scopo delle variabili](https://blog.federicopepe.com/2015/09/variabili-in-processing-creazione-e-personalizzazione/).
