#clase08
## Motivación

Es un [[Árbol Binario (AB)]] ordenado

Construiremos una estructura con nuevas características
- Dada una **llave o clave** queremos asociarle un **valor**
- Si la llave no esta en la EDD, lo sabemos de forma eficiente
- Si la llave está en la EDD; también lo sabemos de forma eficiente
- Podemos agregar, modificar y eliminar **pares llave-valor** de forma eficiente

Esto es un [[Diccionario]]

La idea es construir una EDD con un buen desempeño en **búsqueda, ordenación e inserción**

Podemos modificar a la lista ligada

![[Pasted image 20240908193829.png]]


## Definición

Un **árbol binario de búsqueda (ABB)** es una EDD que almacena **pares (llave, valor)** asociándolos mediante punteros según una estrategia recursiva
1. Un ABB tiene un **nodo** que contiene un a tupla (llave, valor)
2. El nodo tiene hasta dos ABB0's asociados mediante punteros
	- Hijo izquierdo
	- Hijo derecho

Además satisface la **propiedad ABB**: las llaves menores que la llave del nodo están en el sub-árbol izquierdo y las llaves mayores, en el sub-árbol derecho.

Nuevamente estamos aplicando la estrategia [[Dividir para conquistar]]

## Sobre los árboles binarios (en general)

Un árbol binario (de búsqueda o no) cumple que
- Cada nodo `x` tiene **a lo más** un padre `x.p`
- El nodo sin padre se conoce como **raíz**
- Cada nodo `x` tiene **hasta** dos punteros que apuntan a sub-árboles
	- `x.left`
	- `x.right`
	- `x.p` si tiene padre
- Un nodo sin punteros descendentes (sin hijos) se conoce como **hoja**

**Observación**: un árbol binario NO tiene necesariamente nodos con la misma cantidad de hijos

![[Pasted image 20240908194647.png]]

datos ordenados -> dan una lista: peor caso de ABB

### Anatomía del árbol binario

![[Pasted image 20240908194755.png]]
![[Pasted image 20240908194835.png]]

### Algunos teoremas útiles vistos en Matemáticas Discretas

![[Pasted image 20240908195012.png]]

#### Demostraciones de los teoremas

![[Pasted image 20240908195046.png]]
![[Pasted image 20240908195055.png]]
![[Pasted image 20240908195107.png]]

## Operaciones

#clase09

- Queremos búsqueda rápida
- Buscamos lograr un diccionario
	- Queremos garantizar operaciones eficientes para búsqueda, inserción, modificación y eliminación
- Definiendo concretamente estas operaciones mostraremos que un ABB nos sirve como [[Diccionario]]

### El nodo

```c
typedef Struct Nodo
{
	x.key; // llave del nodo
	x.value; // valor del nodo
	Nodo *x.left // puntero al hijo izquierdo
	Nodo *x.right // puntero al hijo derecho
	Nodo *x.p // Puntero al padre
} Nodo;
```

### Búsqueda
- Nos interesa buscar una llave, solo conocemos el nodo raíz
- Comparamos con llave raíz y sabemos que, si esta, esta en uno de los dos subárboles
- Recursivamente repetimos para la raíz del sub-árbol detectado

*Nota posterior*: Se modifica el algoritmo para saber quien es el padre del nodo encontrado

```c
input: ABB A, ABB, padre p, llave a buscar k
output: Tupla con ABB encontrado y su padre

Nodo Search(A,p,k)
{
	if A = null or A.key = k:
		return (A,p)
	if k < A.key:
		return Search(A.left, A, k)
	else
		return Search(A.right, A, k)
}

// llamado inicial es Search(root, k)

// Si retorna (A, null) sabemos que A es la raiz
```

#### Ejemplo de ejecución

![[Pasted image 20240910211639.png]]
![[Pasted image 20240910211654.png]]
![[Pasted image 20240910211702.png]]
![[Pasted image 20240910211710.png]]
### Modificación

Insertar y eliminar un nodo **producen un cambio en la estructura del árbol**
- Se produce un cambio en la **propiedad ABB**
- Los algoritmos deben restaurar la **propiedad ABB** si se incumple

#### Ejemplo de inserción

![[Pasted image 20240910211801.png]]
![[Pasted image 20240910211809.png]]
![[Pasted image 20240910211822.png]]
![[Pasted image 20240910211829.png]]
![[Pasted image 20240910211837.png]]
#### Inserción

```c
input: ABB A, llave k, valor v
Insert (A, k, v):
{
	(B,p) <- Search(A, null, k) // retorna el puntero al lugar del nuevo nodo (es null) y p indica al futuro padre del nodo a insertar
	if B == null:
		B <- nodo vacio
		B.key = k
		Conectar B al padre p en la posición adecuada
	B.value <- v
}

// Este algoritmo mantiene la propiedad ABB al insertar
```

#### Eliminación

Situación más compleja
- Si el nodo a eliminar es hoja o tiene solo un hijo
	- Borrar nodo
	- Si tenia un hijo el hijo lo reemplaza
		- Se mantiene la propiedad ABB
- Si el nodo a eliminar tiene dos hijos
	- PODEMOS REEMPLAZAR POR EL ANTECESOR Y EL SUCESOR DEL NODO A REEMPLAZAR
	- Mirarlo como un arreglo

![[Pasted image 20240910214243.png]]

Entonces nos interesa **encontrar el sucesor/antecesor del nodo extraído**

![[Pasted image 20240910214328.png]]

```c
// Maximo y minimo elementos

Min(A):
	if A.left = Null
		return A
	return Min(A.left)

Max(A):
	if A.right = Null
		return A
	return Max(A.right)
```

```c
Delete(A,k)
{
	(D,p) <- Search(A, null, k) // Permite saber el padre de D
	if D = null
	{
		if (D es hoja)
		{
			D = null
			Se elimina la referencia en p
		}
		else if (D tiene un solo hijo H)
		{
			D = H
			Se actualiza p
		}
		else
		{
			// Swapping
			R <- Min(D.right) // el minimo de ese subABB
			t <- R.right
			D.key <- R.key
			D.value <- R.value
			R <- t
		}
	}
}


// observación: Al borrar un nodo, se debe eliminar la referencia desde su padre

```

#### Sobre el antecesor y el sucesor
- Es fácil encontrarlos preguntando por la raíz
- Pero notamos que no tenemos acceso a `Min` y `Max` si preguntamos por un nodo no raíz

## Complejidad

Todas estas operaciones tienen una complejidad que depende de la **altura** del árbol [[Complejidad Operaciones ABB]]