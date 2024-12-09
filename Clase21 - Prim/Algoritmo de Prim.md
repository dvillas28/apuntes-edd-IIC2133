#clase21

La idea detrás de Prim es utilizar las aristas que cruzan cortes para guiar la construcción del MST

- en Prim, uno se para arriba del nodo y resuelve el problema
- en Kruskal, se mira el problema desde la arista

Utilizamos un Heap con [[Actualización de prioridad]]

Para un grafo $G=(V,E)$ y un nodo inicial $v$
1. Sean $R = \{v\}$ y $\overline{R}=V-R$
2. Sea $e$ la arista de menor costo que cruza de $R$ a $\overline{R}$
3. Sea $u$ el nodo de $e$ que pertenece a $\overline{R}$
4. Agregar $e$ al MST. Eliminar $u$ de $\overline{R}$ y agregarlo a $R$
5. Si quedan elementos en $\overline{R}$, volver al paso 2

Ejecución: revisar apuntes

## Algoritmo

### captura del ppt

![[Pasted image 20241206224727.png]]

### Algoritmo escrito
Inicialmente todos los nodos están a una distancia infinita

$\pi(u)$ padre de u, guardar desde donde llegue
$\alpha(u)$, vecinos de u

```c
Prim(s):
1  Q <- MinHeap() // cola de prioridades
2  T <- lista vacia // MST
3  for u in V - {s}:
4      d[u] <- infinity // las distancias comienzan en infinito
5      pi[u] <- null    // padre de u, guardar desde donde uno llegó, arreglo de predesesores
6      Insert(Q, u)
7  // el nodo inicial s
8  d[s] <- 0     // distancia 0 con si mismo
9  pi[s] <- null // no se llego a el desde ningun nodo
10 Insert(Q,s)
11 
12 while Q no esté vacía:
13     u <- Extract(Q)       // tomamos el nodo con mayor prioriadad
14     T <- T U {(pi[u], u)} // agregamos al MST
15     for v in alpha[u]: // revisamos los vecinos de u
16         if v in Q:
17             if d[v] > cost(u, v):
18                 d[v] <- cost(u, v)
19                 pi[v] <- u
20                 DecreaseKey(Q, v, d[v])
21 return T
```

`Q` usa como prioridad el valor `d[v]`.

`DecreaseKey(Q, v, k)` cambia la prioridad del elemento $v$

## Análisis del algoritmo

### Correctitud

Fijaremos atención a la línea 14 del algoritmo, justo luego de agregar $T$ a una nueva arista. Denotaremos $G_n$ al sub-grafo de $G$ tal que considera solo los primeros $n$ nodos extraídos de $Q$ con todas sus aristas de $G$.

Demostraremos por inducción sobre el número de iteraciones a la propiedad

$P(n) :=$ En la iteración $n$-ésima, la línea 14 guarda en $T$ un MST para el sub-grafo $G_n$

![[Pasted image 20241206223827.png]]

![[Pasted image 20241206223850.png]]

![[Pasted image 20241206223905.png]]

## Complejidad

Considerando que usamos una cola de prioridad implementada como *heap*
- Extracción del más prioritario: $\mathcal{O}(\log V)$
- Actualización de prioridad cuando cambia el costo: $\mathcal{O}(\log V)$

La complejidad en el peor caso viene dado por las iteraciones del **while**
- El *loop* ocurre $|V|$ veces: $\mathcal{O}(V)$
- En cada **loop** se extrae un nodo: $\mathcal{O}(\log V)$
- Cada arista se revisa exactamente una vez: $\mathcal{O}(E)$
- Por cada revisión se hace una actualización de costo: $\mathcal{O}(\log V)$
- Total: $\mathcal{O}((V+E)\log V)$, esto se puede simplificar

Para grafos conexos existe una relación entre $|V|$ y $|E|$
- Si $G$ es un árbol, $E = V - 1$
- Si $G$ es conexo cualquiera, $E \geq V - 1$

Entonces concluimos que $V \in \mathcal{O}(E)$ para grafos conexos
- Luego $(V+E) \in \mathcal{O}(E)$

![[Pasted image 20241206224613.png]]

## Versión mas concreta del algoritmo

![[Pasted image 20241206224402.png]]
