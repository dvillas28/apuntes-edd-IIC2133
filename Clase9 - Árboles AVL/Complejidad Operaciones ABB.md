#clase09 

Hasta ahora, para los [[Arboles binarios de búsqueda]] tenemos las siguientes operaciones
- Búsqueda de valor por llave
- Inserción/Actualización de valor por llave
- Eliminación de una llave y su valor

Todas estas operaciones tienen una complejidad que depende de la **altura** del árbol

![[Pasted image 20240910215853.png]]

## El problema del balance

![[Pasted image 20240910220123.png]]

Dos árboles con una diferencia de altura que impacta en las operaciones definidas 

En un árbol con $n$ nodos, la altura puede ser
- Peor caso: $\mathcal{O}(n)$: Lista ligada
- Cuando el árbol es balanceado es $\mathcal{O}(\log n)$

Buscamos una forma de estudiar balance: Árboles [[Árboles AVL]]

![[Pasted image 20240910220649.png]]