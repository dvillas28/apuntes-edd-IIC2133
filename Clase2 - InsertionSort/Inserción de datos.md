#clase02 

Toda inserción de un dato en una EDD involucra dos pasos
1. Búsqueda de la posición en que se debe insertar el dato
2. Inserción propiamente tal, (puede incluir el mover otros datos)

La complejidad puede variar si usamos [[Arreglo]] o [[Lista Ligada]]

## Inserción usando arreglo ordenado

![[Pasted image 20240815183528.png]]

Para un arreglo de largo $n$
#### Búsqueda
- Requerimos un algoritmo de búsqueda
	- Usando búsqueda binaria, toma tiempo $\mathcal{O}(log(n))$
#### Inserción
También es posible que tengamos que mover desplazar elementos
	- Peor caso, el elemento a insertar es mayor que todos -> hay que desplazar a todos los elementos menores que el: $\mathcal{O}(n)$

**Inserción en arreglos ordenados**: $\mathcal{O}(n)$

## Inserción usando lista (doble) ligada
#### Búsqueda
- Perdemos la indexación, estamos obligados a recorrer la lista ligada completa
	- Esto es $\mathcal{O}(n)$
#### Inserción
- Solo hay que reasignar punteros
	- Esto es $\mathcal{O}(1)$

**Inserción en listas ligadas ordenadas**: $\mathcal{O}(n)$

