#clase07 

Sabemos que un MaxHeap guarda el elemento de mayor prioridad de los primeros en el arreglo
- Entonces si queremos ordenar de menor a mayor, sabemos que este elemento va al final del arreglo
	- **El elemento mas prioritario en el *heap* queda en 0**
	- Luego de intercambiarlo por el ultimo, este queda **ordenado**
- Luego reestablecer la propiedades del *heap* que nos queda (sin el ultimo elemento)
- Y vamos repitiendo este proceso

Se va reduciendo el tamaño del *heap* (`A.heap_size`)

```c
input: arreglo A[0...n-1]

HeapSort(A):
	BuildHeap(A)
	for i = n-1...1: // loop decreciente
		swap(H[0], H[n]) // elem de mas prioridad al final
		A.heap_size -= 1
		SiftDown(A, 0) // Mantener las propiedades del heap

```

El algoritmo termina cuando queda un solo elemento en el *heap*

## Complejidad

- `BuildHeap`: $\mathcal{O}(n)$
- `SiftDown` se repite n veces (por el *loop*): $\mathcal{O}(n\log n)$

Por lo tanto `HeapSort`: $\mathcal{O}(n + n\log n)$ = $\mathcal{O}(n\log n)$

## Mas información

![[Pasted image 20240903200156.png]]

`HeapSort` es independiente a los datos de entrada

Es casi lo mismo que `SelectionSort`, en este caso, se esta ocupando una EDD mas adecuada

Si queremos ordenar de **mayor a menor**, usar un MinHeap

No es estable: como el orden del *heap* es parcial, el orden depende de manipularon los datos en `BuildHeap`

No es envenenable: No tiene peor caso

Cuando usar: más lento que `QuickSort`, en la practica