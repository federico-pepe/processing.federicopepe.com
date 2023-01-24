# Fine (del livello base)

Se siete arrivati a leggere fino a questo post, ho una buona notizia da darvi: abbiamo finito gli argomenti _base_ di Processing. Le fondamenta ci sono tutte e, nella [pagina riassuntiva dedicata](https://blog.federicopepe.com/processing/), potete ripercorrere – tutorial dopo tutorial – il percorso iniziato ben _otto_ mesi fa.

Abbiamo finito? Certo che no. Alcuni argomenti che abbiamo già trattato sarebbero da approfondire e ci sono ancora tantissime cose da imparare e io non ho certo intenzione di fermarmi.

Quando ero partito lo scorso luglio avevo pianificato soltanto dieci post/argomenti di cui volevo parlare che, col tempo, si sono evoluti in ben trenta articoli.

Se devo essere sincero, non ho ancora messo nero su bianco quali saranno i prossimi argomenti ma sto valutando una riorganizzazione dei contenuti e della struttura degli articoli in modo da renderli ancora migliori.

Mi piacerebbe anche ricevere dei suggerimenti sui temi che vorreste che venissero trattati o sulla forma che, secondo voi, dovrebbero avere i contenuti futuri. Potete lasciare un commento a questo post oppure scrivermi via e-mail.

Come sempre, vi invito a [iscrivervi alla newsletter](http://tinyletter.com/creativecoding) dedicata al _creative coding_ per rimanere aggiornati sulle prossime novità.

## Soluzione al "trova l'errore"

![Soluzione: trova l'errore](/assets/images/Processing_trova_lerrore-1024x800.png)

Prima di concludere il post era rimasto in sospeso l'esercizio "trova l'errore" del [post precedente](https://blog.federicopepe.com/2016/02/interazione-tra-oggetti/). Non avendo specificato esattamente qual era il problema nascosto nel codice, prima di darvi la soluzione vorrei assicurarmi che fosse tutto chiaro: come mostrato nell'immagine lo sfondo si è colorato di rosso nonostante i due cerchi non fossero sovrapposti uno all'altro.

Ecco che il problema era dovuto a una svista nel codice della funzione isOver all'interno della classe _Ball.pde:_

`if(distance <= (radius+b.radius)/2)`

è, infatti, necessario dividere per due la somma dei due raggi perché, benché la variabile si chiami _radius_, quando creiamo i nostri cerchi nel constructor, utilizziamo _radius_ come fosse un diametro:

`ellipse(ellipseX, ellipseY, radius, radius);`

Ci eravate arrivati?
