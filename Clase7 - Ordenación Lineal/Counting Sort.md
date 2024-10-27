#clase07 

Considerar una secuencia $A$ de $n$ naturales entre $0$ y $k$
- $\forall a_i \in A$, se tiene que $0\leq a_i \leq k$
- Notamos que no necesariamente se cumple que $n = k-1$
- Podemos tener elementos repetidos en $A$

Se propone un algoritmo que **no compara elementos**
- Para cada dato, contamos cuantos datos son menores que él
	- Esto nos indica la posición final de cada elemento

Si $k \in \mathcal{O}(n)$ entonces este algoritmo será $\Theta(n)$

Es muy importante saber que elementos vamos a ordenar
- Cuantos elementos distintos existen en el arreglo: $k$
	- es el número de valores distintos por cada celda

```c
input: Arreglo A[0...n-1], natural k
output: Arreglo B[0...n-1] ordenado

CountingSort(A, k)
	B[0...n-1]; // Arreglo vacio de n celdas, arreglo a retornar
	C[0...k]; // arreglo de apoyo don0de se lleva la cuenta
	
	// 1. loop de inicializacion de C
	for i = 0...k: 
		C[i] = 0

	// 2. loop para contar los repetidos
	// i: guardan la info de que dato de A es
	// C[i]: numero de copias de i en A
	for j = 0...n-1:
		C[A[j]] = C[A[j]] + 1 // obtener la posicion del ultimo de ese valor

	// 3. loop acumulador de valores:
	// C[i]: numero de elementos menores o iguales a i en A
	for p = 1...k:
		C[p] = C[p] + C[p-1]

	// 4. loop para colocar los elementos
	// A[r]: elemento a colocar
	// C[A[r]] - 1: cuantos elementos menores o iguales a A[r] en A
	// Colocamos a A[r] en esa posicion
	// Luego nos quitamos 1 elemento menor o igual a A[r], ya que ya 
	// lo tenemos colocado
	for r = n-1...0:
		B[C[A[r]] - 1] = A[r] 
		C[A[r]] = C[A[r]] - 1

```

- Complejidad $\mathcal{O}(n+k)$
	- 1° loop: $k$
	- 2° loop: $n$
	- 3° loop: $k$
	- 4° loop: $n$
		- Entonces $\mathcal{O}(2n+2k) = \mathcal{O}(n+k)$
- Si $k\in \mathcal{O}(n)$ entonces `CountingSort` es $\Theta(n)$


3° loop: obtener la posición del ultimo de ese valor

``CountingSort`` necesita saber cuantos datos distintos tenemos
- Su gracia: algoritmo de ordenamiento lineal **estable**