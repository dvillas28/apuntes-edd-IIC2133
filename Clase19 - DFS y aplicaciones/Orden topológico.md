#clase19 

## Definición 

Sea $G$ es un grafo dirigido. Un **orden topológico** de $G$ es una secuencia (orden) de sus nodos $$v_0, v_1, \dots, v_n$$ con $v_i \in V(G)$

tal que 
- todo nodo $u \in V(G)$ aparece en la secuencia

- no hay elementos repetidos en la secuencia

- si $(v_i, v_j) \in E(G)$, entonces $v_i$ aparece antes que $v_j$ en la secuencia

### Proposición

Si $G$ es cíclico, entonces no existe un orden topológico

Podemos usar [[DFS]] para construir un orden topológico de un grafo acíclico

### Ejemplo: Un orden topológico

![[Pasted image 20241115174830.png]]

```c
input: grafo G
output: lista L de nodos en orden topológico

TopSort(G):
1    L <- lista vacia
2    Dfs(G) 
3    Insertar en L nodos en orden decreciente según end
4    return L
```

¿Podemos modificar ``Dfs`` para no tener que ordenar en la línea 3?

```c
input: grafo G
output: lista de nodos L

TopSort(G):
1    L <- lista vacia
2    t <- 1
3    for u in V(G): // seteo de nodos
4        u.start <- 0
5        u.end <- 0
6    for u in V(G):
7        if u.start = 0
8        t <- TopDfsVisit(G, L, u, t)
9    return L

input: grafo G,
	   lista de nodos L,
	   nodo u in V(G),
	   tiempo t
output: tiempo t >= 1

TopDfsVisit(G, L, U, t):
1     u.start <- t
2     t <- t + 1
3     for v in N_g(u):
4         if v.start == 0:
5             t <- TopDfsVisit(G, L, v, t)
6     u.end <- t
7     Insertar u como cabeza de L
8     t <- t + 1
9     return t
```

Al igual que `Dfs`, este algoritmo es $\mathcal{O}(V + E)$

