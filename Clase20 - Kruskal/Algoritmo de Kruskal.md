#clase20

La idea detrás de **Kruskal** es crear un bosque que va convergiendo en un único árbol

Para un grafo $G = (V, E)$, iteramos sobre las aristas $e$ en orden no decreciente de costo
1. Si $e$ genera un ciclo al agregarla a $T$, la ignoramos
2. Si no genera ciclo, se agrega

¿Es necesario revisar **todas** las aristas de $E$?

```c
Kruskal(G):
1 E <- E ordenada por costo, de menor a mayor
2 T <- lista vacía
3 for e in E:
4     if Agregar e a T no forma ciclo:
5         T <- Union(T, e)
6 return T

// este algoritmo usa cortes de manera implícita
```

## Ejemplo de ejecución: conexión con cortes

![[Pasted image 20241206191545.png]]
![[Pasted image 20241206191555.png]]
![[Pasted image 20241206191609.png]]
![[Pasted image 20241206191618.png]]
![[Pasted image 20241206191623.png]]
![[Pasted image 20241206191628.png]]

Dada un arista $(u,v)$ que corresponde chequear
- Podemos considerar un corte dado por $$V_1 = \{w | w \text{ está conectado con } u \text{ con aristas de } T\}$$
- y otro corte dado por $$V_2 = \{w | w \text{ está conectado con } v \text{ con aristas de } T\}$$
Donde $V_2 = V - V_1$

Y agregamos la arista si esta es de corte para esta particion


![[Pasted image 20241206191704.png]]
![[Pasted image 20241206192427.png]]
![[Pasted image 20241206192438.png]]
![[Pasted image 20241206192445.png]]

cualquier arista adicional formaría un ciclo

## Detección de ciclos en el algoritmo

¿Cómo revisar eficientemente lo que plantea la línea 4 del algoritmo?

Podemos utilizar la idea anterior

### Conjuntos

Dada un arista $(u,v)$ podemos considerar los conjuntos
- Nodos conectados con $u$ en $T$ $$V_u = \{w | w \text{ está conectado con } u \text{ con aristas de } T\}$$
- Nodos conectados con $v$ en $T$ $$V_v = \{w | w \text{ está conectado con } v \text{ con aristas de } T\}$$
La arista forma un **ciclo** en $T$ si, y solo si $V_u = V_v$

Estos árboles del bosque $T$ forman [[Conjuntos disjuntos]] y podemos modelarnos eficientemente

- Comenzamos con un conjunto para cada nodo
- Verificamos aristas viendo si sus extremos están en el **mismo conjunto**
- Si no lo están, las agregamos y **unimos** los conjuntos
	- Si lo están, es porque unirlos formaria un ciclo

## Algoritmo con conjuntos disjuntos

```c
Kruskal(G):
1 E <- E ordenada por costo, de menor a mayor
2 for v in V:
3     MakeSet(v): // comenzamos con un conjunto para cada nodo
4 T <- lista vacia
5 for (u,v) in E:
6     if Find(u) != Find(v): // ver si sus extremos estan en el mismo conjunto
7         // no lo estan
8         T <- T U {(u,v)} // la agregamos al MST
9         Union(u,v) // unimos los conjuntos
10return T


```


### Complejidad

Usando la implementación de conjuntos disjuntos

- Ordenar las aristas con un *sorting* eficiente: $\mathcal{O}(E\log E)$
- Construir $V$ conjuntos singleton: $\mathcal{O}(V)$
- Unir conjuntos $V-1$ veces: $\mathcal{O}(V)$
	- **Observación**: si mantenemos un contados a cuantas uniones realizamos durante una ejecución de `Kruskal` y esta resulta ser $\leq V-1$, entonces no es posible construir un MST porque el grafo no es conexo (existe nodos que no están conectados por un camino)
- Buscar $2E$ veces: $\mathcal{O}(E\alpha(n)) = \mathcal{O}(E)$

En total $$\mathcal{O}(E\log E + V + E) = \mathcal{O}(E \log E)$$
Luego, como $E \leq V^2$, tenemos que $\log E \in \mathcal{O}(\log V)$

Por lo que `Kruskal` tiene complejidad $\mathcal{O}(E \log V)$
