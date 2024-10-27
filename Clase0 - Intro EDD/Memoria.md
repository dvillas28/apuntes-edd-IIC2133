#clase00 
## Definiciones

Un ***bit*** es la unidad indivisible de información computacional: puede valer 0 o 1. Es además una celda física indivisible de almacenamiento en un computador
## RAM

Es la **memoria principal** de un computador

La podemos imaginar como un arreglo o matriz de *bits*
- con un cierto numero de columnas (8, 16, 32, 64 *bits*)
- y algunos miles de millones de filas

Cada fila tiene una dirección única
- Es su posición relativa dentro de la tabla
- Natural que parte en 0 y va aumentando de 4 en 4 (si es una RAM de 8 *bits*)

#### Ejemplo. RAM de 1GB, 32 bits

![[Pasted image 20240805151235.png]]

Una fila contiene 32 *bits* -> 4 *bytes*
- En la fila n°0
	- 0-7: *byte* n°1
	- 7-15: *byte* n°2
	- 16-23: *byte* n°3
	- 24-31: *byte* n°4

### [[Variables]]