#clase01 

```c
input: Secuencia de datos A
output: Nueva secuencia de datos B, ordenada

SelectionSort(A):
1 Definir secuencia B, inicialmente vacía
2 Buscar el menor dato x en A
3 Sacar x de A e insertarlo al final de B
4 Si quedan valores en A, volver a la línea 2
  return B
```

## Complejidad

Dado el input $A$, diremos que $|A| = n$ es su largo con $n$ elementos

Tenemos 2 estrategias para determinar la complejidad de ``SelectionSort``

### 1. De forma intuitiva

- Buscar el menor dato en $A$ implica revisar **todos** sus elementos: $\mathcal{O}(n)$
- La búsqueda del menor elemento se hace una vez por dato, i.e., $n$ veces
- Combinando los resultados tenemos $\mathcal{O}(n^2)$

### 2. De forma explícita

- Buscar el elemento menor de $A$ implica revisar $n$ elementos en la primera iteración (se compara uno con todos los demás en el peor caso)
- En la siguiente iteración (peor caso), debemos revisar $n-1$ elementos
- Este proceso de repite hasta agotar $A$ cuando tiene 1 elemento
- El tiempo del algoritmo es la suma de los tiempo de cada iteración

$$T(n) = n + (n-1) + \dots + 2 + 1 = \sum_{i=0}^{n-1}i = \frac{n(n-1)}{2} $$
- Y concluimos que $T(n) \in \mathcal{O}(n^2)$

Para estos enfoques, no estamos tomando en cuenta **la inserción** de los datos

### Costo de la inserción en SelectionSort

Nos interesa la inserción del ultimo elemento

1. [[Lista Ligada]] : Si se cuenta con un puntero al ultimo elemento, la inserción toma $\Theta(1)$ (se puede tomar el puntero al ultimo elemento previo y asignarlo al actual)
2. [[Arreglo]] 
	- si no se supera el espacio reservado para el arreglo: $\Theta(1)$
	- si se agotó el espacio, hay que reubicar todo el arreglo (mover todos los elementos): $\Theta(n)$

Con esto, conocemos las siguientes complejidades

| Operación         | *Array*                                                | *Linked List*                    |
| ----------------- | ------------------------------------------------------ | -------------------------------- |
| Acceso por índice | $\Theta(1)$                                            | $\Theta(n)$                      |
| Inserción (final) | - $\Theta(1)$ sin reubicar<br>- $\Theta(n)$ reubicando | $\Theta(1)$ con puntero al final |
En el caso de los arreglos, en `SelectionSort` sabemos cuanto espacio necesitamos reservar

#### Sobre la complejidad de memoria

Para secuencias de datos muy grandes, puede ser costoso reservar espacio para una copia completa de los datos

`SelectionSort` cumple la siguiente propiedad
	
	$|A| + |B|  =n$
	
Podemos aplicar el algoritmo en un solo arreglo (**Algoritmos *in place***)
- La cantidad de datos **es la misma**

Como se *recicla* el espacio dentro del mismo arreglo para llevar la nueva secuencia B, no es necesario reubicar el arreglo y torda inserción al final de B toma tiempo $\Theta(1)$. Con esto no necesitamos memoria adicional
- Mas precisamente, se necesita $\mathcal{O}(1)$ de memoria adicional

## Síntesis de *SelectionSort*

![[Pasted image 20240814122645.png]]

### Algoritmo *in-place*

![[Pasted image 20240814122702.png]]

1. desde el inicio, hasta uno antes del final
	1. Llego a ``n-2`` ya que comparando de a dos, con esto me evito comprar el ultimo con otro que no existe
2. Definir el mínimo
3. Comparar ``i`` con todos los que tiene adelante, ya que se asume que lo anterior YA ESTA ordenado
- Podemos darle significado a ``i`` e ``j``
	- ``i`` -> posición que estoy ordenando (posición de salida)
	- ``j`` -> posición en el arreglo original


```c
def SelectionSort(list A, int len) -> void:
{
	for pos_a_ordenar in range(0...len-1):
		/*
		posicion del minimo elemento, se supone que lo que va antes
		ya fue ordenado
		*/
		for pos_to_sort in range(0, n-2):
		
			# find the minimum element
			min <- pos_to_sort
			for pos_trav in range(pos_to_sort + 1, ..., n-1):
				if A[pos_trav] < A[min]:
					min <- pos_trav
			# place the minimun at the end of the sorted list
			swap(A[pos_to_sort], A[min])
			# O(n) swaps
}
```


### Mas información. sobre *selection sort*

Info buena para estudiar

![[Pasted image 20240814123908.png]]

- **No es invariante respecto del input**: no tiene mejor caso
- Es un **algoritmo estable**: no altera el orden de los elementos que ya estaban en orden entre si; si los datos de input vienen datos que ya estaban ordenados, en la salida de mantienen en orden