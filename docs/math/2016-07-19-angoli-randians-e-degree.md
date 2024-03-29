---
title: "Angoli: randians() e degrees()"
date: "2016-07-19"
categories: 
  - "processing-math"
tags: 
  - "angoli"
  - "degrees"
  - "radians"
---

Prima di passare a studiare funzioni matematiche come _sin()_, _cos()_ e _tan()_ che, come vedremo, potranno essere molto utili per i nostri esperimenti con Processing, è necessario fare una breve premessa sugli angoli.

La maggior parte delle persone è abituata a misurare gli angoli con i gradi (in inglese _degrees)_: un angolo retto è 90°, un angolo piatto è 180° mentre un angolo giro è 360°. Quando si lavora con la trigonometria è più semplice usare i radianti (in inglese _radians_)_._

Quando usiamo i radianti dobbiamo tenere presente che i valori degli angoli sono espressi in relazione al valore del **π**. Ragionando in radianti, dunque, un angolo retto è π/2, un angolo piatto è π mentre un angolo giro è 2π.

Per chi fosse spaventato da tutto questo e non più molto fresco con l'argomento che stiamo trattando, ricordo che il valore del _pi greco_ è:

> il rapporto tra la misura della lunghezza della circonferenza e la misura della lunghezza del diametro di un cerchio

Per aiutarci, gli sviluppatori di Processing hanno inserito una serie di variabili che possiamo utilizzare nei nostri sketch: **PI**, **QUARTER\_PI**, **HALF\_PI**, **TWO\_PI** (nota bene: devono essere scritte in maiuscolo così come le ho riportate) oltre, ovviamente, a due funzioni che ci permettono di passare dai gradi ai radianti e viceversa:

- La funzione _radians()_ accetta come parametro un valore in gradi e restituisce il valore in radianti.
- La funzione _degrees()_ accetta come parametro un valore in radianti e restituisce i gradi.

Ecco un semplice programma che vi aiuterà a familiarizzare con quanto appena detto:

```java
/*
 * Angoli: radians() e degrees();
 * by Federico Pepe
 *
 */
// COSTANTI
println("QUARTER_PI = "+ QUARTER_PI);
println("HALF_PI = " + HALF_PI);
println("PI = "+ PI);
println("TWO_PI = " + TWO_PI);

// CONVERSIONE
// Gradi -> Radianti
println();
println("Gradi -> Radianti");
println("90 gradi in radianti: " + radians(90));
println("180 gradi in radianti: " + radians(180));

// Radianti -> Gradi
println();
println("Radianti -> Gradi");
println("PI in gradi: " + degrees(PI));
println("TWO_PI in gradi:" + degrees(TWO_PI));
```

Spero di non avervi spaventato con questa parentesi matematica. Prima di procedere oltre ci tengo a sottolineare che al liceo ho avuto sempre molte difficoltà in questa materia quindi cercherò sempre di utilizzare spiegazioni semplici che permettano a chiunque di capire il punto a cui voglio arrivare. Ti auguro, come è successo con me, che la programmazione sia il mezzo per riavvicinarsi alla matematica e, perché no, per capirla un po' di più.
