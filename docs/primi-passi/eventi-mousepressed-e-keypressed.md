# Eventi: mousePressed() e keyPressed()

Un po' alla volta stiamo rendendo i nostri sketch sempre più interattivi grazie ai movimenti del mouse. Per proseguire il percorso della [scorsa lezione](https://blog.federicopepe.com/2015/08/variabili-built-in/) e prima di imparare a creare e utilizzare a nostro piacere delle variabili, argomento che verrà trattato la prossima settimana, oggi parliamo di **eventi**.

Per fare un breve recap: abbiamo imparato come utilizzare [i blocchi di codice _setup()_ e _draw()_](https://blog.federicopepe.com/2015/08/blocchi-di-codice-e-flusso-setup-e-draw/) per suddividere i nostri sketch in due parti e far sì che parte del nostro codice sia eseguito solo all'avvio del programma e una parte, invece, venga processata in un loop costante. Grazie a questo, abbiamo anche visto che Processing è in grado di restituirci in ogni momento la posizione X e Y del mouse e di come possiamo usare questi dati per arricchire i nostri sketch.

Oltre al semplice movimento del mouse possiamo fare in modo che i nostri sketch riconoscano anche altri input disponibili comunemente su un computer: la pressione e il rilascio di un tasto del mouse o della tastiera.

## Cosa sono gli eventi?

Comportandosi in modo simile a _setup()_ e _draw()_, gli eventi sono descritti, anch'essi, come blocchi di codice. La loro particolarità è che il codice scritto al loro interno non viene eseguito automaticamente all'avvio del programma ma  al verificarsi di una condizione specifica come, per l'appunto, il click del mouse. A differenza della funzione draw(), le porzioni di codice all'interno degli eventi non vengono eseguiti in loop ma una volta soltanto.

### Eventi del mouse

La sintassi è simile a quella che abbiamo già visto; per il momento ignoriamo il significato di _void_ e facciamo attenzione all'utilizzo delle maiuscole.

```java
/*
 * Eventi mousePressed() e mouseReleased()
 * by Federico Pepe
 * http://blog.federicopepe.com
 */

void setup() {
  size(500, 500);
  background(255);
}

void draw() {
}

void mousePressed() {
  background(255, 0, 0);
}

void mouseReleased() {
  background(255);
}
```

Analizziamo insieme questo semplice programma:

- dentro **setup()** impostiamo la grandezza della finestra 500x500px e il colore di sfondo bianco.
- la funzione **draw()** per il momento non contiene alcuna riga di codice
- il codice contenuto all'interno di **mousePressed()** verrà eseguito al click del mouse e imposterà rosso come colore di sfondo.
- nel momento in cui verrà rilasciato il tasto del mouse, verrà eseguita la funzione **mouseReleased()** che ripristinerà il bianco come background.

Nel _[Reference](https://processing.org/reference/)_ di Processing trovate anche gli altri eventi legati al mouse:

- [mouseButton](https://processing.org/reference/mouseButton.html)
- [mouseClicked()](https://processing.org/reference/mouseClicked_.html)
- [mouseDragged()](https://processing.org/reference/mouseDragged_.html)
- [mouseMoved()](https://processing.org/reference/mouseMoved_.html)
- [mousePressed()](https://processing.org/reference/mousePressed_.html)
- [mousePressed](https://processing.org/reference/mousePressed.html)
- [mouseReleased()](https://processing.org/reference/mouseReleased_.html)
- [mouseWheel()](https://processing.org/reference/mouseWheel_.html)

È inutile che mi soffermi ora sul fare un esempio per ciascuno di essi: una volta capito il funzionamento è abbastanza intuitivo capire come usare le altre. Vi invito ugualmente a sperimentarle tutte ed, eventualmente, lasciare un commento qualora riscontraste dei problemi.

### Eventi della tastiera

Allo stesso modo e con funzioni simili è possibile determinare se un tasto della tastiera è stato premuto oppure no:

```java
/*
 * Eventi keyPressed() e keyReleased()
 * by Federico Pepe
 * http://blog.federicopepe.com
 */
 
void setup() {
  size(500, 500);
  background(255);
}

void draw() {
}

void keyPressed() {
  background(255, 0, 0);
}

void keyReleased() {
  background(255);
}
```

Se vi state chiedendo se è possibile determinare _quale_ tasto è stato premuto la risposta è ovviamente sì. Per realizzare uno sketch del genere sarebbe, però, necessario introdurre alcuni argomenti che tratteremo in futuro: variabili booleane e cicli if... else if... else... per cui, per oggi, non andrei oltre.
