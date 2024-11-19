#clase18 

## Problema de detectar ciclos

![[Pasted image 20241115105417.png]]

### Caminos

Dado un grafo dirigido $G=(V,E)$, es **camino** $\pi$ es una secuencia de nodos $v_0, v_1, \dots, v_n$ tal que $$\{v_i, v_{i+1} \in E\}$$ para cada $i < n$

Decimos que $\pi := v_o, v_1, \dots, v_n$ es de largo $n$

### Ciclos

Si $n >0$ y $v_0 = v_n$ diremos que $\pi$ es un **ciclo**. Un grafo que posee un ciclo se dice **cíclico**

Para el problema, determinar si hay una secuencia circular de nodos equivale a determinar si el grafo de representación **contiene un ciclo**

## Detección de ciclos

### `Posteriors`

Dadas dos tareas $X$ e $Y$, diremos que $Y$ es **posterior** a $X$ si
- $X \rightarrow Y$ o
- $\exists Z$ tal que $X \rightarrow Z$ e $Y$ es posterior a $Z$

En esencia: $Y$ es posterior a $X$ si $X$ debe realizarse antes que $Y$

```c
input: Grafo G, nodo X in V(G)

Posteriors(G, X):
1 P <- null
2 for Y tal que X -> Y: // como implementar esta linea?
3     P <- Union(P, Y)
4     P <- Posteriors(G, Y)
5 return P
```

### Un llamado de ejemplo

![[Pasted image 20241115111055.png]]

Problema: `Posteriors` no evita nodos ya visitados
- impacto en la complejidad práctica
- si hay un ciclo en el grafo, el algoritmo **no termina**

Necesitamos poder distinguir a los ya visitados: Agregamos un atributo a los nodos

```c
input: Grafo G, nodo X in V(G)

Posteriors(G, X):
1 if X.visited == 1: return null // no visitar los ya visitados
2 X.visited <- 1
3 P <- null
4 for Y tal que X -> Y: // como implementar esta linea?
5     P <- Union(P, Y)
6     P <- Posteriors(G, Y)
7 return P
```

### Un llamado de ejemplo

![[Pasted image 20241115111034.png]]

![[Pasted image 20241115111112.png]]

![[Pasted image 20241115111118.png]]

## `cycleAfter` y `isCyclic`

Para discriminar estos dos casos, se propone la siguiente regla para detección de ciclos

Si el nodo $Y$ que vamos a visitar ya fue visitado:
1. Si estamos en un nodo posterior a $Y$, **hay ciclo**
2. Si no, entonces **esta arista no forma ciclo** (pueden haber en otras zonas)

Importante: hasta que `Posteriors(G, X)` retorne, todos los visitados que se marcan son posteriores a $X$

Agregamos colores para distinguir el **tipo de visitado**
- blanco = no visitado
- gris = visitado posterior
- negro = visitado no posterior

```c
// Este algoritmo decide si hay un ciclo partiendo desde X

input: Grafo G, nodo X in V(G)

cycleAfter(G, X):
1     if X.color = gris: return true // visitado posterior -> hay ciclo
2     if X.color = negro: return false // visitdo no posterior -> no hay ciclo
3     X.color <- gris // visitamos el nodo
4     for Y tal que X -> Y:
5         if cycleAfter(G, Y): return true
6     X.color <- negro // no hay ciclo despues de X, es un visitado no posterior
7     return false
```

```c
// Este algoritmo decide si hay un ciclo en el grafo

input: Grafo G

isCyclic(G):
1    for X in V(G):
2        if X.color != blanco: // nos saltamos los nodos ya visitados
3            continue
4        if CycleAfter(G,X):
5            return true
6    return false

```

El algoritmo `isCyclic` sigue una estrategia de **búsqueda en profundidad** [[DFS]]