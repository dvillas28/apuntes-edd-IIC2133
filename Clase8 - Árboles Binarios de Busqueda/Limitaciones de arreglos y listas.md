#clase08 
## Acceso y búsqueda

En una [[Lista Ligada]] de llaves
- No tenemos **acceso por índice** de forma eficiente
- La búsqueda, incluso en el caso ordenado es $\mathcal{O}(n)$

En un [[Arreglo]] de llaves
- Hay un **acceso por índice** en $\mathcal{O}(1)$
- La búsqueda en general es $\mathcal{O}(n)$
	- Para el caso ordenado, podemos lograrla en $\mathcal{O}(\log n)$

### Inserción

En la lista ligada
- Para insertar solo se necesita reasignar punteros (pocos)
- La inserción de un nuevo elemento es $\mathcal{O}(1)$

En el arreglo
- Insertar un elemento puede gatillar un **desplazamiento de datos**
- En promedio, esta inserción es $\mathcal{O}(n)$
