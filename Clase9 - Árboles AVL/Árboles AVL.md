## Propiedad de *balance*

Se deben cumplir 2 condiciones
1. Asegurar que la altura de un árbol con $n$ nodos sea $\mathcal{O}(\log n)$
2. Ser fácil de mantener (punto limitante)
	- Llamaremos al (re)balanceo después de las operaciones
	- Queremos complejidad **no mayor** que $\mathcal{O}(\log n)$
	- De esa forma no alteramos la complejidad de las operaciones previamente definidas

## Árboles AVL (Adelson-Velsky y Landis)

![[Pasted image 20240910221501.png]]

Es un modelo de balance de ABB

**Los AVL son [[Arboles binarios de búsqueda]] balanceados**

### Definición

Un ABB esta **AVL-balanceado** si:
1. Las alturas de sus hijos difieren **a lo más en 1 entre si**
2. Cada hijo esta **AVL-balanceado**

#### ejemplo

Árbol AVL-balanceado

![[Pasted image 20240910221900.png]]

Árbol desbalanceado

![[Pasted image 20240910222202.png]]

## Rotaciones
### Rotaciones Simples
### Rotaciones Dobles

## Complejidad de las rotaciones

Una rotación tiene **costo constante**
- rotación simple: se cambian 3 punteros: $\mathcal{O}(1)$
- rotación doble: se cambian 5 punteros: $\mathcal{O}(1)$

Además, al rotar para restaurar balance de X, este se resuelve sin crear un nuevo balance
- No se aumentan las diferencias de altura respecto al resto del árbol
- en el peor caso, se realiza a lo más **una rotación** (simple o doble) **por inserción**

Gracias a esto, para un árbol de altura $h$ una inserción contempla
- Inserción como tal: $\mathcal{O}(h)$
- Detección de nodos que participan de la rotación (si aplica): $\mathcal{O}(1)$
- En el peor caso aplicar rotación: $\mathcal{O}(1)$
- Estos pasos se realizan consecutivamente: $\mathcal{O}(h)$

## Altura de un árbol AVL en función de $n$

Considerar la relación inversa: como $n$ depende de $h$
- Para un árbol AVT $T$
	- ¿Cuál es el máximo número de nodos de $T$ si tiene altura $h$?
	- ¿Y el minimo?

Si probamos un crecimiento exponencial para $n$ en función de $h$, probaremos que la altura está acotada por $\log n$

### Caso máximo

![[Pasted image 20240920211515.png]]

### Caso minimo

![[Pasted image 20240920211609.png]]
![[Pasted image 20240920211653.png]]

## Teorema importante

Todo árbol AVL con $n$ nodos tiene una altura $h$ tal que $$h \in \mathcal{O}(\log n)$$