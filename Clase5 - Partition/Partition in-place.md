#clase05 

```c
input: Secuencia A[0, ..., n-1], indices i, f
output: Indice del pivote aleatorio en la secuencia ordenada

// j: posicion del pivote
// va cambiando hasta que toma la posicion que debe

Partition(A, i, f):
1 x <- random({i,...,f})
2 p <- A[x]
3 swap(A[x], A[f]) // colocamos al pivote al final
4 j <- i // definimos la posicion del pivote
5 for k = i...(f-1):
6     if A[k] < p: // si el elemento es menor que el pivote
7         swap(A[j], A[k]) // corremos al pivote a la derecha
8         j <- j + 1
9 swap(A[j], A[f]) // depositamos al pivote en su posicion ordenada
10 return j
```

Con este cambio, `QuickSort` usa memoria adicional $\mathcal{O}(1)$

- La partición se da cuando movemos todos los elementos cuando vamos intercambiando elementos en la linea 7, efectivamente vamos dejando lo menores al pivote a la izquierda
	- Luego de terminada el *loop*, j representa la **posición ordenada del pivote**

## Correctitud

### Demostración (terminación)

La condición de terminación es que se termine el for de la linea 5
- Se realizan i-f-1 iteraciones, es decir se hace un for sobre un set finito de datos
- Por lo tanto `Partition` termina

### Demostración (correctitud)

A demostrar que el pivote se encuentra en su posición ordenada en la secuencia
- El pivote se coloca en la posición j (línea 9), debemos probar que se encuentra en su posición ordenada

$P(n):=$ Luego de la n-esima iteración, `A[i, ..., j-1]` contiene solo elementos menores a `p` y `A[j, ...., k-1]` contiene solo elementos mayores o iguales a `p`

- **Caso Base**: $P(1)$: Es el estado de `A[i, ..., k-1]` luego de la 1° iteración (``k = i``). Tenemos dos casos (línea 6)
	1. Si `A[i] < p`, como tenemos que `i = j`, `A[i]` se mantiene en esa posición, y `j, k` aumentan en 1 (linea8 y siguiente iteración del *loop*)
		- Luego `A[i, ...,j-1]` solo contiene un elemento (`A[i]`), el cual es menor a `p`.
		- `A[j, ..., k-1]` no tiene ningún elemento pues `j=k` (no hay elementos mayores a `p` en la 1° iteración)
	2. Si `A[i] >= p`, tenemos que `A[i]` se mantiene es esa posición (no se cumple el condicional de la línea 6), `j` no aumenta, pero `k` si
		- Luego `A[i, ...,j-1]` no contiene ningún elemento (no hay elementos menores a `p` en la 1° iteración) 
		- `A[j...k-1]` contiene solamente a `A[i]` el cual es mayor o igual a `p`

- **Hipotesís inductiva**: Suponemos que se cumple luego de la n-ésima iteración, `A[i...j-1]` solo contiene elementos menores a `p` y `A[j...k-1]` solo contiene elementos mayores o iguales a `p`

- **Tesis Inductiva**: Al termino de la $n+1$-ésima iteración, pueden haber ocurrido dos casos
	1.  Si `A[i] < p`,  `A[i]` se intercambia con `A[k]`, y `j, k` aumentan en 1 (linea8 y siguiente iteración del *loop*)
		- Luego `A[i, ...,j-1]`, que por HI cumple que contiene elementos menores a `p` , se le agrega `A[i]` y sigue conteniendo elementos menores
		- `A[j, ..., k-1]`, por HI sigue conteniendo elementos mayores o iguales a `p`
	2.  Si `A[i] >= p`,  `A[i]` se mantiene en esa posición, y `j` no aumenta, pero `k` si lo hace
		- Luego `A[i, ...,j-1]`, por HI sigue conteniendo elementos menores a `p`
		- `A[j, ..., k-1]`, que por HI sigue conteniendo elementos mayores o iguales a `p`, se le agrega `A[i]` y sigue conteniendo elementos mayores o iguales