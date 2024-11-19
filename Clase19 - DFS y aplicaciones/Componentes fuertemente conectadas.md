#clase19 

## Definición

Sea $G$ un grafo dirigido. Una **componente fuertemente conectada (CFC)** en un conjunto máximal de nodos $C \subseteq V(G)$ tal que dados $u, v \in C$, existe un camino dirigido desde $u$ hasta $v$.
### Proposición

Si $G$ es cíclico y los nodos de $B \subseteq V(G)$ forman un ciclo, entonces existe una componente fuertemente conectada $C$ tal que $B \subseteq C$

Los nodos de un ciclo pertenecen a la misma CFC

### Proposición

Un grafo $G$ acíclico tiene 0 componentes fuertemente conectadas
- Ejemplo: grafo de dos nodos


![[Pasted image 20241115181634.png]]

![[Pasted image 20241115181655.png]]

## Proposición

![[Pasted image 20241115182246.png]]

El grafo $G$ y su [[Grafo Transpuesto]] y $G^T$ tienen las mismas componentes fuertemente conectadas

## Algoritmo para determinar CFC

Podemos construir un orden de los nodos de $G$ según tiempos de término

![[Pasted image 20241116163108.png]]

![[Pasted image 20241116163150.png]]

```c
input: Grafo G

Kosaraju(G):
1     L <- TopSort(G)
2     for u in L:
3         Assign(u, u)

input: Grafo G,
       nodo u in V(G),
       nodo representante r

Assign(G, u, R):
1     if u.rep == null:
2         u.rep <- r
3         for v in N_{G^T}(u):
4             Assign(G, v, r)

```

Observación: NO podemos interpretar L como orden topológico. Es un orden que se construye de la misma forma

El algoritmo de *Kosaraju* se basa en las propiedades del siguiente grafo

#### Definición

Dado un grafo $G$ dirigido, sean $C_1, \dots, C_K$ sus componentes fuertemente conectadas. Se define el **grafo de componentes** $G^{CFC}$ según
- $V(G^{CFC}) = \{C_1, \dots, C_k\}$
- Si $(u,v) \in E(G)$ y $u \in C_i, v \in C_j$, entonces $(C_i, C_j) \in E(G^{CFC})$

**Teorema**: El grafo de componentes $G^{CFC}$ es un grafo dirigido acíclico

**Corolario**: El grafo de componentes $G^{CFC}$ tiene un orden topológico

![[Pasted image 20241116164041.png]]