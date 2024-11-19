#clase18

Forma de representar información

Se pueden tener grafos dirigidos con autoloops

El punto de partida define el alcance sobre el grafo dirigido
para grafo no dirigido depende de si este es conexo o no

## Grafos dirigidos

Un **grafo dirigido** es un par $G = (V, E)$, donde $V$ es el conjunto de **nodos** y $E$ es el conjunto de **aristas** de la forma $(u,v)$, con $u, v \in V$

![[Pasted image 20241115103424.png]]

## Grafos no dirigidos

Un **grafo dirigido** es un par $G = (V, E)$, donde $V$ es el conjunto de **nodos** y $E$ es el conjunto de **aristas** de la forma $(u,v)$, con $u, v \in V$ y $u \neq v$

![[Pasted image 20241115103510.png]]

Usaremos grafos no dirigidos cuando importe agrupar pares de nodos vecinos

## Complejidad de algoritmo sobre grafos

- Usaremos $|V|$ y $|E|$ como parámetros de tamaño, abreviados como $V$ y $E$

¿Es mejor un algoritmo $\mathcal{O}(V)$ o $\mathcal{O}(E)$?

Depende. Tenemos dos situaciones extremas
- $|E|  =0$
- Grafo completo (todas las aristas posibles)

## Representación de grafos

Tenemos dos formas

1. **Lista de adyacencia**. La celda $i$ de la lista tiene una lista con los vecinos $j$ tales que $(i,j)$ es arista en el grafo
2. **Matriz de adyacencia**: La celda $[i][j]$ indica si $(i,j)$ existe en el grafo

La información de los nodos se almacenan en las dimensiones, mientras que las aristas son los datos adicionales

 La complejidad en grados puede depender de qué representación se usa

![[Pasted image 20241115105344.png]]

[[Detección de Ciclos en un Grafo]]