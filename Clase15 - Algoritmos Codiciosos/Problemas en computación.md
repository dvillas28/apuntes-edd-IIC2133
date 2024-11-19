#clase15 

![[Pasted image 20241109224617.png]]

## Problema computacional

Un **problema computacional** es un problema que puede resolverse con un [[Algoritmos]]

Distinguimos 5 tipos de problemas computacionales

1. Problemas de decisión
	1. Pregunta binaria (sí o no)
	2. Ejemplo: *"Determinar si el tablero de Sudoku T tiene solución"*
2. Problemas de búsqueda
	1. Secuencia de estados hasta alcanzar un estado objetivo
	2. Ejemplo: *"Determinar un camino para salir del laberinto L desde $\Theta$"*
3. Problemas de conteo
	1. Número de soluciones diferentes
	2. Ejemplo: *"Determinar el número de configuraciones válidas de 8 reinas"*
4. Problemas de optimización
	1. Mejor solución de acuerdo a alguna métrica
	2. Ejemplo: *"Determinar el camino más corto de A a B en el mapa G"*
5. Problemas de función
	1. Solución explícita
	2. Ejemplo: "*Determinar una solución del Sudoku T*"

## *Backtracking* y optimización

[[Backtracking]] es una técnica de diseño muy flexible

Podemos atacar muchos tipos de problemas con esta, PERO, no es la mejor solución para algunos

*Backtracking* no suele ser la mejor opción a los problemas de **optimización**

## Ejemplo: Problema de la mochila con objetos fraccionables

Tenemos $n$ objetos y una mochila

- los objetos tienen pesos $\{w_1, \dots, w_n\}$
- los objetos tienen ganancias por unidad de peso $\{p_1, \dots, p_n\}$
- la mochila tiene una capacidad $m$, en peso
- incluir una fracción $x_k$ del objeto $k$ proporciona ganancia $p_{k}x_{k}$

Interesa llenar la mochila cumpliendo tres condiciones

- Queremos maximizar la ganancia total $$\text{max}\sum_{k=1}^np_{k}x_{k}$$ Esta es la **función objetivo**

- No podemos exceder la capacidad de la mochila $$\sum_{k=1}^nw_{k}x_{k}\leq m$$
- Las fracciones deben cumplir $$0 \leq x_k \leq 1, 1 \leq k \leq n$$
Una **solución factible** es $\{x_1, \dots, x_n\}$ que cumple las dos últimas condiciones. Una **solución óptima** es una solución factible que maximiza la función objetivo

¿Cómo escoger los valores $x_k$ adecuados para encontrar una solución óptima? [[Algoritmos Codiciosos]]


