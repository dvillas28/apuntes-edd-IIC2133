#clase14 

Supongamos que nos interesa salir de un laberinto dado que estamos en $\Theta$

![[Pasted image 20241109210610.png]]

Podemos resolver este problema con *backtracking*

Planteamos el problema como un CSP

- Variables
- Dominios
- Restricciones
- Definición de éxito

Caracterizamos por $\Theta$ la posición actual

En cada nueva posición $\Theta$ solo podemos elegir dar un paso en las direcciones libres y distintas de aquella de la cual venimos

![[Pasted image 20241109210757.png]]

Debemos hacer *backtrack* cuando llegamos a un camino sin salida: solo muros y celdas ya visitadas

![[Pasted image 20241109210852.png]]

¿Hasta dónde nos arrepentimos con el *backtrack*? Hasta llegar a una celda ya recorrida con alguna dirección que no hayamos probado

Luego, logramos llegar a una solución que encuentra la salida

![[Pasted image 20241109211045.png]]

#### Algoritmo

Le agregamos etiquetas a las posiciones, de modo que sabemos cuáles hemos visitado (**visited**). Todas comienzan con **nonvisited** y la salida se marca como **exit**

```c
input: Conjunto de variables sin asignar X, posición x, dominios D, restricciones R

isSolvable(X, x, D, R):
1 if x = exit; return true
2 if visited: return false   // esta nos indica hasta donde devolverse
3 x <- visited
4 for v in {N, E, S, W}:
5     if x + v != wall:
6         x <- x + v
7         if isSolvable(X, x, D, R):
8             return true
9         x <- nonvisited
10 return false
```

