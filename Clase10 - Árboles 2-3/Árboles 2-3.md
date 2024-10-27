#clase10 

## El problema del balance

Tenemos nuestra primera definición de balance para árboles binarios
- Propiedad AVL definida recursivamente: Diferencia de alturas entre hermano a lo más de 1

Podemos dar otra definición: Que todas las hojas **estén a la misma profundidad**, y que esta sea $\mathcal{O}(\log n)$

Usaremos una mezcla entre árboles binarios y ternarios. Tendremos una nueva estructura que incluye
- Dos tipos de nodos
	- **2-Nodos**: Tendrán una llave, y si no son hojas, tendrán **2 hijos**
	- **3-Nodos**: Tendrán dos llaves distintas y ordenadas, y si no son hojas tendrán 3 hijos
- Esto permitirá tener las hojas a la misma profundidad
- Y además garantizará profundidad $\mathcal{O}(\log n)$ al almacenar $n$ llaves

## Definición

Un **árbol de búsqueda 2-3** es una EDD que almacena **(llave, valor)** según
1. Un árbol 2-3 tiene un nodo que puede ser
	- **2-nodo**: con una llave
	- **3-nodo**: con dos llaves distintas y ordenadas

2. El nodo puede no tener hijos o tener **exactamente**
	- 2 hijos árboles 2-3 si es un 2-nodo
	- 3 hijos árboles 2-3 si es un 3-nodo
	- Esto garantiza **hojas al mismo nivel** y **niveles completos**

3. y que además, satisface la **propiedad de árboles 2-3**
	- Si es 2-nodo con llave $k$
		- las llaves $k'$ del hijo izquierdo son $k'<k$ 
		- las llaves $k''$ del hijo derecho son $k<k''$
	- Si es 3-nodo con llaves $k_1<k_2$
		- las llaves $k'$ del hijo izquierdo son $k'<k_1$
		- las llaves $k''$ del hijo central son $k_1<k''<k_2$
		- las llaves $k'''$ del hijo derecho son $k_2<k'''$
## Estructura de los nodos

![[Pasted image 20241014163822.png]]

![[Pasted image 20241014163829.png]]

### ejemplo de un árbol 2-3

![[Pasted image 20241014163850.png]]

- Tal como en un [[Arboles binarios de búsqueda]], el orden de las llaves está implícito

## Búsqueda en árbol 2-3

Podemos buscar elementos comparando llaves recursivamente
En el peor caso, tenemos que comparar dos llaves por nodo
##### ejemplo 1

![[Pasted image 20241014164041.png]]

##### ejemplo 2

![[Pasted image 20241014164136.png]]

## Inserción en 2-3

¿Cómo insertar llaves manteniendo la profundidad pareja?

Se sigue la siguiente estrategia

```
Se inserta como llave múltiple en una hoja existente

if la hoja era 2-nodo
	queda como 3-nodo y terminamos

elif la hoja era 3-nodo
	queda como 4-nodo (con 3 llaves) POR AHORA

	la llave central del 4-nodo sube como llave múltiple al padre (split)

	Se repite la modificación de forma recursiva hasta la raíz
```

El árbol solo crece en altura cuando la raíz se llena al recibir una llave desde un hijo

### ejemplo de creación de árbol 2-3

*Consultar los apuntes escritos para ver el ejemplo*

## Síntesis final

![[Pasted image 20241014164826.png]]