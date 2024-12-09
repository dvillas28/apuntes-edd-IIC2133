#clase22 

El algoritmo de Dijkstra encuentra las rutas más baratas desde $s$
- Solo a aquellos vértices alcanzables desde $s$
- Puede haber más de una ruta con el mismo costo
	- El algoritmo encuentra **una**
- Dijkstra NO revisita nodos
- Se basa en un recorrido BFS del grafo

Super buenos videos para entender:
- [(522) How Dijkstra's Algorithm Works - YouTube](https://www.youtube.com/watch?v=EFg3u_E6eHU)
- [(522) Shortest Path Algorithms Explained (Dijkstra's & Bellman-Ford) - YouTube](https://www.youtube.com/watch?v=j0OUwduDOS0)

Es un [[Algoritmos Codiciosos]]

Además, el problema de rutas más cortas tiene una **sub-estructura óptima**

Dada una ruta entre $v_0$ y $v_k$
- Si $p = v_0, v_1, \dots, v_k$ es una ruta de costo mínimo
- Entonces la sub-ruta $$p_{ij}=v_i, \dots, v_j$$ $$ i \leq j \leq k$$
Es una ruta más corta de $v_i$ a $v_j$

## Algoritmo

![[Pasted image 20241207171441.png]]


```c
Dijkstra(s):
	for u in V - {s}:
		u.color <- blanco // nodos aun no descubiertos
		d[u] <- inf       // arreglo de costos, como no tenemos info sobre los otros nodos, estos comienzan a distancia infinita
		pi[u] <- null     // arreglo usado para reconstruir el camino

	s.color <- gris       // comenzar explorando el nodo inicial
	d[s] <- 0             // solo sabemos que cuesta 0 desde el nodo inicial

	Q <- MinHeap()        // cola de prioridades basada en el arreglo de costos d
	Insert(Q, s)

	while Q no está vacia:
		u <- Extract(Q)  // extraemos el nodo con el menor costo asociado actual
		for v in alpha(u): // y visitamos los nodos vecinos
			if v.color == blanco or v.color == gris: // si es un nodo aun no visitado o pendiente
				if d[v] > d[u] + cost(u,v): // vemos si movernos a v desde u cuesta menos que el costo actual de moverse a v
					// si es que si
					d[v] <- d[u] + cost(u,v) // actualizamos el costo
					pi[v] <- u // indicamos que se llega a v desde u (u es el predecesor de v)
					DecreaseKey(Q, v, d[v]) // como el costo de llegar a v disminuyo, actualizamos el heap de prioridades
				if v.color = blanco: // si es un nodo aun no visitado
					v.color <- gris // lo marcamos como pendiente
					Insert(Q, v) // y insertamos el vecino al heap de prioridad

		// una vez analizamos todos los vecinos de u, ya podemos marcarlo como visitado y explorado
		u.color <- negro
```

- En `d[k]` se almacena el mejor tiempo estimado que toma llegar al nodo `k`
- `Q` usa como prioridad el valor `d[k]` para ir explorando los nodos
- Cada vez que comenzamos a explorar un nodo `k`, estamos garantizando que `d[k]` es el menor costo que tomó llegar hasta `k`

Si queremos reconstruir el camino
- Si al explorar un nodo, mantenemos un registro del nodo desde el cual llegamos al actual, podemos luego reconstruir el camino desde el nodo destino para atrás
- Para esto tenemos el arreglo de predecesores $\pi$
## Análisis del algoritmo

### Finitud

![[Pasted image 20241207170538.png]]

### Correctitud

![[Pasted image 20241207170557.png]]
![[Pasted image 20241207170612.png]]
![[Pasted image 20241207170631.png]]
![[Pasted image 20241207170643.png]]

## Complejidad

En el peor caso, el algoritmo realiza
- $\mathcal{O}(V)$ operaciones `Extract`
- $\mathcal{O}(E)$ operaciones `d[v] <- d[u] + cost(u, v)` (que actualizan la cola)

Si la cola se implementa como un *heap* binario
- La operación `Extract` es $\mathcal{O}(\log V)$
- La actualización de costos (prioridad) en el *heap* es $\mathcal{O}(\log V)$

El algoritmo de Dijkstra toma tiempo $\mathcal{O}((V+E)\log V)$

## Variantes

El algoritmo se puede adaptar para resolver otros problemas comunes

- Rutas más cortas en grafos acíclicos
- Rutas más cortas de un vértice a otro (específico)
- Rutas más cortas entre **todos** los pares de vértices
- Rutas más cortas en grafos Euclidianos

## Consideración adicional

Este algoritmo esta diseñado para grafos con pesos **positivos**
- Si se introduce un peso negativo, es posible que se encuentren costos menores para llegar a un nodo, pero como el algoritmo no revisita nodos, se retorna un resultado incorrecto. [[Dijkstra con costos negativos ]]