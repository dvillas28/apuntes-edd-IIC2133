#clase20 

## Definición

Una colección de **conjuntos disjuntos** $\{S_1, \dots, \S_n\}$ es una [[Estructuras de Datos]] que permite
- Identificar a qué conjunto **pertenece** un elemento (pertenencia)
- **Unir** conjuntos $S_i, S_j$ formando un nuevo conjunto

Para representar los conjuntos se usa a un **representante**
- es un elemento cualquiera de $S_i$ denotado por $rep(S_i)$
- la consulta del representante debe ser consistente si no hay cambios en $S_i$: se deberia entregar el mismo resultado siempre
- Cada elemento de $S_i$ tiene una referencia a $rep(S_i)$

Entonces, dos conjuntos $S$ y $T$ son iguales si y solo si $rep(S) = rep(T)$


## Usando listas ligadas

![[Pasted image 20241206193348.png]]

El problema es que las operaciones de búsqueda y unión se vuelven muy complejas
- búsqueda: debería ser eficiente, ya que se tiene un puntero al representante
- unión: surge complejidad por el cambio de representante en cada elemento de un conjunto

## `Find` y `Union`

Supondremos que las operaciones de búsqueda y unión son de la forma
- `Find(A)`: entrega el conjunto al que pertenece $A$
- `Union(A)`: entrega un conjunto resultante de unir los conjuntos de $A$ y $B$

Además, supondremos que en un estado inicial, tenemos $n$ conjuntos con **un solo elemento cada uno** (*singleton*)
## Conjuntos como árboles

Podemos representar los conjuntos como árboles donde los caminos llevan al representante
![[Pasted image 20241206194709.png]]

Entonces, `Union` corresponde a cambiar el autoloop del representante de un conjunto: $\mathcal{O}(1)$

![[Pasted image 20241206194750.png]]

`Find` requiere recorrer punteros, por lo que las dos opciones no seran equivalentes
- Entonces unimos el árbol más corto al más largo

![[Pasted image 20241206195046.png]]

pero podemos modificar los punteros para que se simplifiquen las rutas
![[Pasted image 20241206195130.png]]

## Almacenamiento

Podemos almacenar los árboles en un único arreglo de referencias

Tendremos que `A[k]` es el padre `k`

![[Pasted image 20241206195232.png]]

Si `A[k] = 0`, entonces estamos en el *autoloop* revisando el padre del representante, que es el mismo
## Complejidad de `Find`

Depende de que elemento de busca (que tan lejos estamos del representante)

- Se puede demostrar que para un conjunto de $n$ elementos, con rutas simplificadas, `Find` toma tiempo $\mathcal{O}(\alpha(n))$
- $\alpha(n)$ es la función inversa de Ackermann, y crece **extremadamente lento** $$\alpha(n) = 4, 2048 \leq n \leq 16^{512}$$ por lo que para cualquier aplicación practica, podemos considerar que $\alpha(n) \in \mathcal{O}(1)$