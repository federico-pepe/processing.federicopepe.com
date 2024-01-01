# Le novità di Processing 3

!!! warning "Attenzione"
    Processing è un linguaggio di programmazione in costante evoluzione. Fate sempre riferimento al sito ufficiale [www.processing.org](https://www.processing.org) per verificare gli ultimi aggiornamenti disponibili.

Il 30 settembre 2015 è stata rilasciata una nuova major release di Processing: la versione 3. Prendendo spunto dal [video ufficiale](https://vimeo.com/140600280) con cui [Daniel Shiffman](http://www.shiffman.net) illustra le principali novità del software, ho deciso di scrivere questo post, soprattutto per chi ha difficoltà con l'inglese.

## Nuova icona, nuovo editor

Una volta scaricato e installato sul vostro computer noterete subito che Processing 3 ha una nuova icona. Le novità grafiche non sono, però, finite qui: quando avviate il programma comparirà un _welcome screen_ che, la prima volta, vi consiglierà di creare una nuova cartella _sketchbook_ dove tenere i vostri sketch. È consigliabile tenere separati i programmi realizzati per la versione 2 e la versione 3 perché, a causa di alcuni cambiamenti nel linguaggio, alcuni vecchi sketch potrebbero non funzionare.

![Welcome screen di Processing 3](/assets/images/Processing_3_welcome_screen-742x1024.png)

Oltre alla nuova icona e all'inedito welcome screen, una delle prime cose che notiamo è il design dell'editor che è stato completamente rivisto: anche in questa finestra troviamo delle nuove icone e, finalmente, i numeri delle linee di codice a sinistra oltre a delle nuove tab in basso.

[![Il nuovo editor di Processing 3](/assets/images/Processing_3_new_editor-1024x902.png)](https://blog.federicopepe.com/wp-content/uploads/2015/10/Processing_3_new_editor.png)

## Error Checking e Warning

Il nuovo sistema di error checking sarà di grande aiuto soprattutto per chi sta iniziando a programmare: i messaggi di errore sono stati rivisti in modo da essere più "leggibili". Di default verranno visualizzati nella console gli errori mentre digitiamo il codice invece che alla pressione del comando Run come accadeva nella versione precedente.

In questo modo sarà molto più difficile dimenticarsi un _punto e virgola_ alla fine di un'istruzione o una parentesi. I programmatori più esperti possono disabilitare questa opzione andando nel pannello delle preferenze e deselezionando _Continuously check for errors._

Nel caso in cui nel nostro codice ci fosse più di un errore, cliccando sulla nuova tab **Errors**, presente nella parte inferiore della finestra,abbiamo una panoramica di tutti i problemi presenti nel nostro codice.

Un'altra novità sono i **Warning**: non si tratta di veri e propri errori ma di messaggi che ci avvisano che nel nostro codice c'è qualcosa di strano. Ad esempio, se creiamo e inizializziamo una variabile che, però, non usiamo da nessuna parte nel nostro programma, ci verrà restituito un messaggio di avviso. A differenza degli errori, evidenziati in rosso, i warning vengono sottolineati in giallo.

## Code completion

Questa opzione non è attiva di default ma è selezionabile nelle preferenze: grazie a essa, premendo _Ctrl+spazio_ l'editor ci darà dei suggerimenti su come completare il nostro codice. Se utilizzate OS X, verificate che la combinazione Ctrl+spazio sia libera perché su alcuni computer potrebbe lanciare la ricerca Spotlight_._

[![Processing 3: code completion](/assets/images/Processing_3_code_completion-880x1024.png)](https://blog.federicopepe.com/wp-content/uploads/2015/10/Processing_3_code_completion.png)

## Tweak

Oltre alla modalità _Run_, in Processing 3 è stata aggiunta la modalità **Tweak**. Una volta lanciato il nostro sketch in questa modalità (su Mac la scorciatoia è **⇧⌘T**), possiamo modificare "in diretta" alcuni parametri del nostro sketch e avere un feedback immediato senza interrompere il programma.

Una volta stoppata la modalità tweak, l'editor ci chiederà se vogliamo mantenere le modifiche apportate al nostro codice oppure se vogliamo tornare alla versione originale.

## Debugger

Anche questa novità è mutuata da altri linguaggi di programmazione: attivando il debugger, il pulsante a forma di insetto presente in alto a destra, possiamo far girare il nostro programma una linea alla volta verificando, dunque, in quali punti viene generato un errore. Per capire meglio come sfruttare questa novità, consiglio [questo video](https://vimeo.com/140134398), sempre realizzato da Dan che ne illustra il funzionamento nel dettaglio.

## OpenGL, fullScreen() e pixelDensity()

Prima di parlare di due nuove funzioni molto interessanti sottolineo che gli sviluppatori hanno lavorato molto per rendere Processing 3 molto più veloce rispetto alla versione precedente. Questo risultato è dovuto principalmente alla nuova engine di rendering che non si basa più su _PApplet_, una tecnologia ormai in disuso, ma su **OpenGL**.

Venendo alle nuove funzioni, _fullScreen()_ sostituisce _size(displayWidth, displayHeight)_ e ci permette di far girare i nostri sketch a pieno schermo. Questa nuova funzione, però, non fa soltanto questo: se abbiamo uno schermo collegato possiamo passare il parametro _fullScreen(1)_ oppure _fullScreen(2)_ per decidere su quale display verrà presentato il nostro programma.

Se, invece, abbiamo più schermi collegati al computer con _fullScreen(SPAN)_ lo sketch si adatterà automaticamente al setup multidisplay occupando tutto lo spazio disponibile. Una cosa importante da sottolineare è, grazie a questa nuova funzione, _size()_ non accetta più variabili ma solo parametri hard-coded.

Se siete possessori di un computer con schermo Retina, la nuova funzione _pixelDensity()_ vi piacerà molto: grazie a essa possiamo aumentare la densità di pixel del nostro sketch per adattarlo all'alta risoluzione del nostro schermo. La differenza è davvero notevole!

## Contribution Manager

![Processing 3 - Contribution Manager](/assets/images/Processing-3-Contribution-Manager-1024x934.png)Se utilizzate librerie o tool aggiuntivi nei vostri sketch, il nuovo **Contribution Manager** sarà una novità che vi piacerà parecchio. In questa nuova finestra potrete cercare, installare, disinstallare e aggiornare tutti gli strumenti aggiuntivi che utilizzate e verificarne la compatibilità con la versione di Processing che state utilizzando.

## Tutte le altre novità

Come anticipavo all'inizio del post, lo scopo di questo articolo era fare una panoramica sulle principali novità introdotte in quest'ultima versione di Processing. Se siete interessati a scoprire nel dettaglio quali sono tutte le novità introdotte in quest'ultima versione, vi consiglio di visitare [questa pagina su GitHub](https://github.com/processing/processing/wiki/Changes-in-3.0).
