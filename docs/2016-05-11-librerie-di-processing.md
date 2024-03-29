---
title: "Librerie: estendere le funzionalità di Processing"
date: "2016-05-11"
categories: 
  - "processing-libs"
tags: 
  - "contributed-libraries"
  - "contribution-manager"
  - "librerie"
coverImage: "Processing_Contribution_Manager.png"
---

# Librerie: estendere le funzionalità di Processing

È possibile estendere le funzionalità di base di Processing utilizzando delle **librerie esterne**. Una libreria non è altro che un insieme di _classi_, _funzioni_ e _variabili_ pensate e progettate con il preciso scopo di semplificare l'esecuzione di determinate operazioni che, se programmate da zero, renderebbero il nostro programma troppo verboso.

L'idea che sta alla base delle librerie è di fare in modo di non appesantire troppo i programmi che non le richiedono motivo per cui, quando decidiamo di usarne una, dobbiamo usare una sintassi ben precisa per dire al programma "carica questa libreria perché ho intenzione di usarla".

## Librerie built-in

Esistono una serie di librerie che sono incluse già all'interno del pacchetto di Processing:

- **Serial:** quando dobbiamo interfacciare il nostro sketch con hardware esterno attraverso la porta seriale
- **Network:** per creare applicazioni client e server comunicanti via internet
- **PDF:** per grafiche di alta qualità esportate in formato PDF
- **DXF:** per esportare grafiche in formato DXF

Ci sono poi le librerie **Sound** e **Video** che sono sviluppate dalla Processing Foundation ma che è necessario scaricare attraverso il menu `Sketch > Import Library > Add Library`.

## Contributed Libraries

![Librerie disponibili nel Contribution Manager](/assets/images/Processing_Contribution_Manager-1024x931.png)

Oltre quelle sviluppate dalla Processing Foundation, esistono numerose librerie di terze parti. Partendo dal menu `Sketch > Import Library > Add Library` è possibile scaricarle e installarle sul nostro computer. Le _contributed libraries_ che compaiono nel **Contribution Manager** rispettano degli standard ben precisi che possono essere consultati sul [repository ufficiale di GitHub](https://github.com/processing/processing/wiki/Library-Overview) e sono progettate per segnalare automaticamente eventuali aggiornamenti.

Scorrendo rapidamente la lista di tutte le librerie disponibili potete notare la quantità di funzionalità che possono essere aggiunte ai nostri programmi; per fare degli esempi: integrazione di messaggi MIDI, OSC, creazione di GUI, utilizzo di hardware esterno (Leap Motion, Microsoft Kinect), simulazioni di engine 2D e molto altro.

In futuro dedicherò alcuni articoli e guide a quelle più conosciute e utilizzate, nel frattempo, però, potete consultare gli esempi che trovate nel menu `File > Examples > Libraries / Contributed Libraries` che vengono installati insieme alla libreria.

## Installare librerie manualmente

Tutte le librerie vengono installate all'interno della cartella `~/Documents/Processing/libraries` (su Mac) o `Documents/Processing` (su Windows). Nel caso in cui vogliate installare delle librerie di terze parti non presenti nel Contribution Manager che, generalmente, si trovano in formato _.jar_ è sufficiente copiare i file nella cartella di riferimento. È buona norma inserire il file .jar in una sottocartella con lo stesso nome. Una volta completata l'installazione è necessario riavviare Processing per poterle utilizzare.

## Utilizzare le librerie installate

Il comando di cui parlavo all'inizio del post per dire al nostro programma "carica la libreria perché voglio utilizzarla" è molto semplice: `import` a cui bisogna aggiungere i componenti che vogliamo caricare.

![Processing Importa Libreria](/assets/images/Processing_Import_library.png)

Attraverso il menu `Sketch > Import Library`, selezionando la libreria, Processing aggiungerà automaticamente il codice necessario nel nostro sketch.
