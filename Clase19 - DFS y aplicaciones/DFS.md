#clase19

- *Depth First Search*
- la estrategia es avanzar por aristas adyacentes hasta más no poder 
- luego de agotar esa ruta, se retrocede y se exploran otras
- todas las rutas se exploran en **profundidad**

## Un ejemplo ya visto

![[Pasted image 20241115113516.png]]

## Algoritmo DFS básico

Queremos un algoritmo que solo recorra el grafo
- idea: no visitar nodos ya visitados
- unico efecto en el grafo es cambiar colores
- lo usaremos como base para nuevos grafos

Usaremos el código de colores, de una manera general

- **blanco**: no visitado
- **gris**: visitado y tiene vecinos (*está en proceso*)
- **negro**: visitado y todos sus vecinos fueron visitados (*está terminado*)

```c
input: Grafo G
Dfs(G):
1    for u in V(G): // loop de seteo
2        u.color <- blanco
3    for u in V(G) // loop de recorido
4        if u.color == blanco:
5            DfsVisit(G,u)


input: Grafo G, nodo u in V(G)
DfsVisit(G,u)
1    u.color <- gris 
2    for v in N_g(U): // N_g(u): vecinos de u (nodos apuntados por aristas desde u)
3       if v.color == blanco:
4           DfsVisit(G,v)
5    u.color <- negro
```

`DfsVisit` solo hace recursión cuando el nodo siguiente no ha sido visitado

## Análisis de complejidad

Para ambas implementaciones de $N_g$

- Cada nodo solo inicializa blanco: $\mathcal{O}(V)$
- Cada nodo solo se visita (coloreado gris) una vez: $\mathcal{O}(V)$
- Cada arista se *recorre* una vez al chequear el vecino: $\mathcal{O}(E)$

`Dfs` toma tiempo $\mathcal{O}(V + E)$, i.e. es lineal en $|G|$


## Aplicaciones con `Dfs`

### `Dfs` con tiempo de inicio y término

Nos da una noción de orden

Además de usar colores, *recordaremos* cuándo se hicieron esos cambios

- Cuando se visita un nodo, se pinta **gris**
	- además definiremos un **tiempo de descubrimiento o inicio**
- Cuando se completa un nodo, se pinta **negro**
	- además definiremos un **tiempo de término o finalización**

Los tiempo de inicio y termino serán números correlativos ($1,2,\dots$)

```c
input: Grafo G
Dfs(G):
1    t <- 1
2    for u in V(G): // loop de seteo
3        u.start <- 0
4        u.end <- 0
5    for u in V(G) // loop de recorido
6        if u.start == 0: // analizar solo los que aun no hemos visitado
7            t <- DfsVisit(G, u, t)


input: Grafo G, nodo u in V(G), tiempo t
output: tiempo t >= 1
DfsVisit(G,u)
1    u.start <- t
2    t <- t + 1
3    for v in N_g(U): // N_g(u): vecinos de u (nodos apuntados por aristas desde u)
4       if v.start == 0:
5           DfsVisit(G, v, t)
6    u.end <- t // cuando ya se procesaron todos los vecinos de u
7    t <- t + 1
8    return t     
```

**Importante**: el recorrido DFS puede generar un **bosque** de árboles independientes.
- Esto es dependiendo del nodo en que se inicia el DFS

### Propiedades de los tiempos

Dado $G$ y $u,v \in G$, diremos que $u$ es **descendiente** de $v$ al ejecutar `Dfs`($G$) si $u$ es visitado por primera vez luego de $v$ y antes de que $v$ sea terminado. En tal caso diremos que ambos pertenecen al mismo **árbol DFS**

#### Proposición

Dado $G$ y $u,v \in V(G)$, luego de ejecutar `Dfs`($G$) se definen los intervalos $$I_u = \{ u.start, \dots, u.end\}$$ $$I_v = \{ v.start, \dots, v.end\}$$
Estos intervalos cumplen una de las siguientes propiedades

- $I_u \cup I_v = \emptyset$ (no están en el mismo árbol DFS)

- $I_u \subset I_v$ ($u$ es descendiente de $v$)

- $I_v \subset I_u$ ($v$ es descendiente de $u$)

#### Tipos de aristas en DFS

Con la convención anterior nos permite distinguir aristas al recorrer con DFS

Dado $G$ y $u,v \in V(G)$, luego de ejecutar `Dfs`($G$), la arista $(u,v)$ puede ser
- **Arista de árbol** si $v$ fue descubierto al transitar $(u,v)$

- **Arista hacia atrás** si $u$ es descendiente de $v$ en un árbol DFS

- **Arista hacia adelante** si $(u,v)$ no es de árbol y $v$ es descendiente de $u$

- **Arista cruzada** en otro caso

##### Proposición

Un grafo $G$ es acíclico si, y solo si, `Dfs`($G$) no produce aristas hacia atrás


### Ejemplos

![[Pasted image 20241115170137.png]]

![[Pasted image 20241115170144.png]]

TODO: no entiendo esto?