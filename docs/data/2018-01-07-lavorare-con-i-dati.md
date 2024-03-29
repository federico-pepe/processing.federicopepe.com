---
title: "Lavorare con i dati"
date: "2018-01-07"
categories: 
  - "data"
coverImage: "Processing-lavorare-con-dati.jpg"
---

Nel mondo digitale tutto è un insieme di **dati**: che si tratti di un testo, una foto oppure un video, stiamo parlando di una sequenza di 1 e 0 che chiamiamo comunemente _file_.

Con questo post inauguro una nuovo capitolo su questo blog in cui scopriremo insieme come utilizzare Processing per lavorare con file e dati.

Quale potrebbe essere il vantaggio di utilizzare un linguaggio di programmazione per questo genere di attività? Perché non possiamo utilizzare strumenti per grafici o designer come Photoshop o Illustrator? La risposta è semplice: uno dei vantaggi dei computer rispetto alla mente umana è che sono in grado di processare velocemente numeri ed eseguire operazioni ripetitive e complesse molto velocemente.

La vista di un file di Excel pieno di righe e colonne può scatenare il panico nelle persone sane di mente ma per un software non servono altro che _due cicli for_ per accedere al contenuto di ciascuna cella. Quello che impareremo a fare sarà, poi, assegnare quel contenuto a una (o più) variabili e il gioco è fatto.

Pensiamo alle _visualizzazioni di dati_ che negli ultimi anni sono diventate onnipresenti su siti web, riviste e quotidiani. Il loro successo è dovuto al fatto che, grazie a un linguaggio di tipo visuale, rendono più accessibile il contenuto della storia, anche quando include una grande mole di dati. A differenza della _carta stampata_ realizzando un'infografica con Processing si apre un ventaglio di possibilità: possiamo renderla interattiva, in 3D, può essere su uno schermo oppure proiettata su una parete.

## Tipi di dato

Quali saranno i tipi di dati su cui lavoreremo? Abbiamo già avuto modo di parlare di [immagini e pixel](https://blog.federicopepe.com/2017/03/array-pixel-loadpixels-updatepixels/) (tema che approfondiremo), ma in questa sezione ci concentreremo su:

- File di testo (.txt)
- Tabelle di dati di Excel (.csv, .tsv)
- Pagine web (.html)
- Feed (.xml)
- API (.json)
