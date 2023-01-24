# Array bidimensionali: esercizio media difficoltà (soluzione)


Ecco la soluzione all'esercizio di difficoltà media proposto nell'articolo [Array bidimensionali](https://blog.federicopepe.com/2017/02/array-bidimensionali-processing/).

## Esercizio:

Siete in grado di modificare lo script affinché, ad esempio, modificando i valori all’interno di size() mi venga disegnata sempre una scacchiera di 8×8 che occupi l’intera grandezza della finestra (anche quando non è quadrata)?

## Soluzione:

```java
/*
 * Array bidimensionali - esercizio media difficoltà
 * Federico Pepe, 19.02.2017
 * http://blog.federicopepe.com/processing
*/

int[][] scacchiera = { 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1}, 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1}, 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1}, 
  {1, 0, 1, 0, 1, 0, 1, 0}, 
  {0, 1, 0, 1, 0, 1, 0, 1} };

void setup() {
  size(480, 700);
  
  int rows = 8;
  int cols = 8;
  
  float tileSizeX = width/rows;
  float tileSizeY = height/cols;
  
  for (int i = 0; i < rows; i++) {
    for(int j = 0; j < cols; j++) {
      if(scacchiera[i][j] == 0) {
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

![Esercizio array bidimensionale](/assets/images/Processing-Array-Bidimensionali-Esercizio-medio-1024x540.png)
