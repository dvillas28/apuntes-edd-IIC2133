#clase22 

- Algoritmo de **búsqueda en amplitud**
- *Breadth First Search*
- la estrategia es revisar los vecinos inmediatos de un nodo, y leugo seguir con los vecinos de estos
- BFS recorre en base a la **distancia desde un nodo inicial**

Para el problema considerado, $\delta$ será la distancia desde el punto de inicio hasta cada nodo

Luego, por definición, $\delta$ es la **menor distancia** de $A$ (un nodo inicial) a cualquier nodo.

## Ejemplo de Ejecución

En los apuntes...

BFS descubre los nodos a través del menor número de aristas
- Siempre se visitan primero los nodos a distancia $\delta = K$
- Luego se llega a los que están a distancia $\delta = K + 1$

Debemos asegurar que los nodos son descubiertos en el orden adecuado

¿Cómo distinguir entre descubiertos y no descubiertos?
## Implementación

### Implementación en Python

```python
from collections import deque

def bfs(grafo: Grafo, inicio: Nodo):
    """
    Implementacion para un grafo representado como lista de adyacencia
    """

    # lista de los nodos ya visitados, esto es necesario para evitar que caigamos el loops en el grafo
    visitados = []

    queue = deque([inicio]) # recordar que el queue es FIFO

    # mientras queden elementos en el queue, seguiremos recorriendo
    while len(queue) > 0:
        # elegimos el nodo a visitar
        nodo = queue.popleft() # sacamos el primero de la cola

        # vemos si no ha sido visitado antes
        if nodo in visitados:
            continue # proseguir a la siguente iteracion

        # visitar nodo
        print(nodo)
        visitados.append(nodo)

        # ahora agregamos los vecinos del nodo al queue
        for vecino in grafo[nodo]:
            if vecino not in visitados:
                queue.append(vecino)

    return visitados # recorrido final
```


Podemos distinguir los nodos con *colores*
- blanco: no descubierto
- gris: descubierto con vecinos no descubiertos (pendientes)
- negro: descubierto con vecinos descubiertos (terminado)

Como nos interesa descubrir nodos **en orden**, hay que almacenar los recién descubiertos
- Usamos una cola FIFO ([[Queues]])
- Cuando descubrimos un nodo, lo agregamos al final de la cola
- Para revisar nuevos vecinos, sacamos el nodo prioritario

```c
input: vertice de inicio s

BFS(s):
    for u in V - {s}:
        u.color <- blanco // marcar todos los nodos menos s como no visitados
        u.delta <- inf // setear como distancia infinita
        pi[u] <- null // aqui dejaremos la representacion de un árbol de rutas mas cortas desde s

	s.color <- gris // marcar el nodo inicial s como 'pendiente'
	s.delta <- 0    // y su distancia inicial 0
	pi[s] <- 0

	Q <- Queue() // cola FIFO vacía
	Insert(Q, s)

	while Q no está vacia:
		u <- Extract(Q) // sacamos el primero de la cola
		for v in alpha[u]: // recorremos los vecinos del nodo extraido
			if v.color == blanco: // si recien lo descubrimos...
				v.color <- gris // lo dejamos como pendiente
				v.delta <- u.delta + 1 // y marcamos la distancia
				
				pi[v] <- u
				Insert(Q, v) // agregamos el vecino al queue
		
		u.color <- negro // una vez recorremos todos los vecinos no visitados previamente y los agregamos al queue, marcamos ese nodo como terminado
```

Problema: BFS no funciona para rutas con costos. 