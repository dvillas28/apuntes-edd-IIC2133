#clase23

Para encontrar las rutas **más baratas** desde **una sola fuente** seguiremos la siguiente estrategia

- Buscamos rutas más cortas desde $s$ con a lo más 1 arista
- Luego, con a los más 2 aristas
- Luego, con a lo más 3 aristas
- ...

Esta estrategia aprovecha un enfoque de [[Programación dinámica]]
1. Buscamos las rutas más cortas con a lo más $k$ aristas
2. Podemos utilizar las rutas más cortas con a lo más $k-1$ aristas

¿Hasta que largo de $k$ es necesario iterar?

## Subestructura óptima en rutas

Dado un grafo dirigido $G$ y nodos $x, y \in V(G)$, diremos que $p: v_0, v_1, \dots, v_n$ es un camino dirigido de $x$ hasta $y$ si
- $(v_i, v_{i+1}) \in E(G)$ para cada $0 \leq i \leq n-1$
- $v_0 = x$ y $v_n = y$

También denotaremos a $p$ como $v_0 \rightarrow v_1 \rightarrow \dots \rightarrow v_n$ Si existe un camino dirigido $p$ de $x$ hasta $y$ y los denotaremos por $x \leadsto_p y$. Además, el largo del camino dirigido $p$ es $|p| = n$

**Proposición**: Si el camino dirigido $u \leadsto_p x \rightarrow y$ es una ruta más corta $u$ a $y$, entonces $p$ es una ruta más corta de $u$ a $x$

![[Pasted image 20241207201921.png]]

Considerar la $k$-pésima iteración

Estamos analizando las rutas más cortas con largo $|p| \leq k$

Sean $s \leadsto u$ y $s \leadsto v$ las rutas más cortas con $|p| \leq k-1$

Para cada arista $(u,v) \in E$ hay que comparar dos rutas
- $s \leadsto u \rightarrow v$
- $s \leadsto v$ (la misma ruta ya conocida, sin cambios)

Tal comparación determina si la arista $(u,v)$ se incluye en la ruta óptima $s \leadsto v$ para obtener una de largo $\leq k$  (Notemos que esta comparación es esencialmente la misma que en Dijkstra)

Nos interesa conocer el largo máximo de una ruta más corta $p$ desde $s$ a cualquier nodo de $G$. Para esto definimos una herramienta util

## Ciclos con costos negativos

Sea $G$ un grafo no dirigido con costos. Un ciclo $p: v_0, v_1, \dots, v_n$ de $G$ es un **ciclo con costo negativo** si $$\text{cost}(p) = \sum_{i=0}^{n-1}\text{cost}(v_i, v_{i+1}) < 0$$
![[Pasted image 20241207203453.png]]

![[Pasted image 20241207203440.png]]


![[Pasted image 20241207203525.png]]

Dado un camino más corto $p$ de $s$ a $u$
- Sabemos que $G$ no tiene ciclos con costo negativo alcanzables desde $s$ (ya que impiden la existencia de rutas más cortas)
- $p$ tampoco tiene ciclos de costo no negativo

Luego la ruta mas larga $p$ no tiene ciclos
- Sabemos que no repite vértices ($p$ es simple)
- La ruta más larga posible tendría $|p| = |V|$

Luego los posibles valores de $k$ están en el rango $1 \dots |V| -1$

## Algoritmo

![[Pasted image 20241207203836.png]]

## Detalle importante

Dijimos que $|V| -1$ iteraciones eran suficientes porque no habían ciclos

Lo que interesa no es que el **grafo sea acíclico**

Importa que **desde la fuente** no se llegue a ningún **ciclo con costo negativo** (pues es el único tipo de ciclo que puede aparecer). ¿Cómo chequeamos que no hayan ciclos de costo negativo?

![[Pasted image 20241207204154.png]]

Una versión del algoritmo para detectar ciclos de costo negativo

![[Pasted image 20241207204208.png]]

## Complejidad

Complejidad de `ValidBellmanFord`

Actualización de costos
- $\mathcal{O}(V)$ iteraciones
	- Cada una hace $\mathcal{O}(E)$ comparaciones
- Total: $\mathcal{O}(VE)$
- Chequeo de ciclos
	- $\mathcal{O}(E)$ comparaciones

Por lo que Bellman-Ford es un algoritmo $\mathcal{O}(VE)$ en el peor caso