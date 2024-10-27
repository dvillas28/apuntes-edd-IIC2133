#clase06 

Vamos a utilizar una mirada conceptual de lo que es un *heap*
- Se implementa en código con un arreglo
- Visualmente usaremos un árbol binario

Es una estructura jerárquica con un orden parcial

Dividir el problema, usando un enfoque de sub-estructuras ordenadas
- Enfoque recursivo
- Estructura recursiva + algoritmos recursivos
- Cada sub-estructura debe tener cierta forma

Usaremos como base una EDD recursiva: [[Árbol Binario (AB)]]

## Max heap binario

Un **Max heap binario** H es un AB tal que
- ``H.left`` y ``H.right`` son Max heaps binarios
- `H.key` > `H.left.key`
- `H.key` > `H.right.key`

- Usamos un MinHeap para tomar elementos con la menor prioridad primero
- Usamos un MaxHeap para tomar elementos con la mayor prioridad primero

Estas condiciones son las **propiedades del heap**

![[Pasted image 20240828201831.png]]

![[Pasted image 20240828201839.png]]

## Balance en heaps

En un principio, un heap no tiene condiciones sobre su altura

Almacenaremos los heaps complétandolos por nivel
- Primero se llena el nivel antes de seguir bajando
	- Antes de agregar un nivel, el ultimo disponible se haya completado
- i.e. arboles binarios casi-llenos

OBS: Si el arbol binario es ***completo*** y tiene n nodos, entonces se relaciona con la altura h de manera $$n = 2^h - 1$$
Esto NO ocurre necesariamente aqui

![[Pasted image 20240828202430.png]]

Buscamos mantener los heaps **balanceados**. Esto permite
- Minimizar la altura del árbol representado
- Implementar el heap de forma compacta como **arreglo**

## *Heaps* implementados como arreglos


![[Pasted image 20240903200914.png]]

La representación permite recorrer descendientes sin punteros
- El elemento $H[k]$ es padre de $H[2k+1]$ y $H[2k+2]$
- El padre de $H[k]$ es $H[\lfloor\frac{k-1}{2}\rfloor]$

También permite ubicar elementos del nivel $h$ sin punteros
- El primer elemento del nivel $h$ es $A[2^h - 1]$
- Los $2^h$ elementos consecutivos corresponden al nivel $h$

![[Pasted image 20240828202901.png]]

Caso $h=2$
- $A[2^2 -1] = A[3] = 7$
- tenemos $2^2 = 4$ elementos consecutivos en el nivel $h=2$
![[Pasted image 20240828203104.png]]

## Asegurar balance en *heaps*

Ahora que contamos con una representación compacta, nos interesa asegurar el **balance** del *heap*

Inserción y Extracción
1. Efectuar ambas operaciones manteniendo un árbol binario casi-lleno
2. Reestablecer las propiedades del *heap*
### Extracción

#### Ejemplo de uso

Queremos sacar al elemento mas prioritario
- La cabeza del *heap*
- El primer elemento: $A[0]$

![[Pasted image 20240828204036.png]]

Al sacarlo, el árbol **ya no esta casi lleno**
Movemos el ultimo elemento al inicio $A[0] = A[9]$

![[Pasted image 20240828204129.png]]

El árbol esta casi lleno, pero no se cumple la propiedad del heap

![[Pasted image 20240828204201.png]]

De la nueva cabeza, seleccionamos el hijo con mayor prioridad e intercambiamos 

![[Pasted image 20240828204252.png]]

![[Pasted image 20240828204300.png]]

Y Repetimos el proceso recursivamente

![[Pasted image 20240828204317.png]]

![[Pasted image 20240828204336.png]]

![[Pasted image 20240828204347.png]]

El *heap* queda balanceado después de la extracción

#### Algoritmos

El proceso anterior se muestra en los siguientes algoritmos `Extract` y `SiftDown`

```c
input: heap representado como arreglo H[0...n-1]
output: elemento mas prioritario

Extract(H):
	i <- última celda no vacía de H
	best <- H[0] // la cabeza del heap es el elem + prioritario
	H[0] <- H[i] // mover el ultimo elemento al inicio
	H[i] <- Null // dejar vacia esa pos
	SiftDown(H,0) // reubicar recursivamente la nueva cabeza
	// para que cumpla las props del heap
	return best // retornamos el elemento de mayor propiedad
```

Notamos que en `Extract` intercambiamos antes de reestablecer la propiedad del heap con `SiftDown`

```c
input: heap representado como arreglo H[0...n-1],i
	   indice i tal que0<= i <= n-1

SiftDown(H, i):
	if i tiene hijos:
		j <- hijo de i con mayor prioridad
		if H[j] > H[i]: // si el hijo tiene mayor prioridad
			swap(H[j], H[i]) // intercambiarlos
			SiftDown(H,j) // repetir hasta llegar a un nodo sin hijos
	else:
		return
```

Para un arreglo de largo $n$, este algoritmo es $\mathcal{O}(\log n)$ (gracias a que es un árbol casi-lleno)
### Inserción

Se sigue la misma idea, la inserción se hace al final y se reubica recursivamente con `SiftUp`

```c
input: heap como arreglo H[0...n-1],
	   elemento e a ingresar

Insert(H, e):
	i <- primera celda vacía de H
	H[i] <- e // se inserta al final del arreglo
	SiftUp(H, i) // ubicar correctamente este elemento

```

```c
input: heap como arreglo H[0...n-1]

SiftUp(H, i):
	if i tiene padre:
		j <- floor((i-1)/2)
		if H[j] < H[i]: // si el padre tiene menor prioridad
			swap(H[j], H[i]) // intercambiarlos
			SiftUp(H, j) // repetir hasta llegar a un nodo sin padre
	else:
		return
```

Para un arreglo de largo $n$, este algoritmo es $\mathcal{O}(\log n)$

## Construcción de un *heap*

#clase07

Dado un arreglo A, tenemos dos formas para convertirlo en un Heap
- Iterar sobre cada elemento, insertando sobre un heap originalmente vacío (Con el método `Heap.Insert`): Requiere memoria adicional
- Utilizar `SiftDown` para ciertos elementos de A (*in-place*)

```c
input: arreglo A[0...n-1]

BuildHeap(A): // Crea un heap en tiempo O(n)
	for i = floor(n/2)-1...0: // loop decreciente
		SiftDown(A, i)

/* 
los elementos de A en los cuales no se llama
directamenet SiftDown son hojas del último nivel del árbol
*/
```

Complejidad:
- Asintotica directa es $\mathcal{O}(n\log n)$
- Se puede demostrar que una mejor cota es $\mathcal{O}(n)$

Usamos *heaps* para implementar [[Heap Sort]]