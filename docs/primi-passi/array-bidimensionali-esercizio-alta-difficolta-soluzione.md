# Array bidimensionali: esercizio alta difficoltà (soluzione)


Ecco la soluzione all’esercizio di difficoltà media proposto nell’articolo [Array bidimensionali](https://blog.federicopepe.com/2017/02/array-bidimensionali-processing/).

## Esercizio

Partendo dalla soluzione all’esercizio di [difficoltà media](https://blog.federicopepe.com/2017/02/array-bidimensionali-esercizio-media-difficolta-soluzione/), sareste in grado di modificarlo ulteriormente per fare in modo che la griglia non sia necessariamente 8×8?

## Soluzione

```java
/*
 * Array bidimensionali: esercizio alta difficoltà
 * Federico Pepe, 19.02.2017
 * http://blog.federicopepe.com/processing
 */

void setup() {
  size(480, 480);

  int rows = 16;
  int cols = 16;
  
  boolean[][] scacchiera = new boolean[rows][cols];

  boolean tileColor = false;

  // Riempi i dati
  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      scacchiera[i][j] = tileColor;
      tileColor = !tileColor;
    }
    if(cols % 2 == 0) {
      tileColor = !tileColor;
    }
  }
 

  // Disegna la scacchiera
  float tileSizeX = width/rows;
  float tileSizeY = height/cols;

  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      if (scacchiera[i][j]) {
        fill(0);
      } else {
        fill(255);
      }
      rect(i*tileSizeX, j*tileSizeY, tileSizeX, tileSizeY);
    }
  }
}

void draw() {
}
```

![Processing 2D Array hard](/assets/images/Processing-Array-Bidimensionali-Esercizio-difficile-1024x657.png)
