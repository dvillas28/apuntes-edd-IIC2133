#clase04 
## Caso introductorio - La mediana

Nos interesa encontrar la mediana en un grupo de valores

#### Definición
Dana una secuencia ordenada de $n$ valores $a_0, a_1, \dots, a_{n-1}$, llamaremos **mediana** al valor $M_e$ dado por 

- Si $n$ es impar: $$M_e = a_{\lfloor\frac{n}{2}\rfloor}$$
- Si $n$ es par: $$M_e = \frac{a_{\frac{n}{2}} + a_{\frac{n}{2}-1}}{2}$$
La mediana es tal que en la secuencia hay la misma cantidad de elementos mayores y menores a ella

##### 1° estrategia recursiva
Tomar un elemento de la secuencia al cual se le llama **pivote**
1. ¿El pivote es la mediana?
2. Si no, ¿la mediana es mayor o menor al pivote?

-> necesitamos el # de elementos menores y mayores que el pivote
--> Si el pivote termina en la posición al medio del arreglo, es la mediana

- Notamos que al aplicar este algoritmo, el pivote termina la posición ordenada

## ``Partition``

Si suponemos que no hay elementos iguales al pivote, elegir un pivote $p$ **particiona** la secuencia en
- Elementos mayores al pivote: M = {$a_i$ | $a_i$ > $p$}
- Elementos menores al pivote: m = {$a_i$ | $a_i$ < $p$}

Si reubicamos los elementos de la secuencia de forma que
- Primero se colocan los elementos de m
- Luego se coloca $p$
- Finalmente se colocan los elementos de M
Entonces esta claro que $p$ está en su posición ordenada

### El algoritmo

Suponemos que no hay elementos repetidos en la secuencia

```c
input: Secuencia A[0, ..., n-1], indices i,f
output: Indice del pivote aleatorio en la secuencia ordenada

Partition(A, i, f);
1 p <- pivote aleatorio en A[i, f]
2 m, M <- secuencias vacias
3 Insertar p en M // decision conveniente
4 for x in A[i, f]
5     if x < p : Insertar x en m
6     else if x > p : Insertar x en M
7 A[i, f] <- Concat(m, M)
8 return i + |m|
```

- Notar que esto retorna la posición correcta de p
	- El retorno es la cantidad de elementos a la izquierda de $p$ en la secuencia ordenada
#### Análisis de complejidad
- Inserciones en arreglos y listas: $\mathcal{O}(1)$
- Se realiza una inserción por elemento en el arreglo: $\mathcal{O}(n)$
- ``Concat``:
	- $\mathcal{O}(1)$ en listas
	- $\mathcal{O}(n)$ en arreglos

Luego tenemos $\mathcal{O}(n)$ + $\mathcal{O}(1)$ = $\mathcal{O}(n)$ y $\mathcal{O}(n)$ + $\mathcal{O}(n)$ = $\mathcal{O}(n)$

Entonces ``Partition`` es $\mathcal{O}(n)$
Además usa complejidad $\mathcal{O}(n)$ de memoria adicional

Ahora nos aprovechamos de este algoritmo para crear particiones para encontrar la mediana de una secuencia

### ``Median``

Suponemos que no hay elementos repetidos en la secuencia

```c
input: Secuencia A[0, ..., n-1]
output: Elemento central de A

Median(A);
1 i <- 0
2 f <- n-1
3 x <- Partition(A, i, f) // recordar que retorna el indice de un random
4 while x no es el centro:
5	// ajuste de rango
6	if x < centro : i <- x + 1
7	else: f <- x-1
8	x <- Partition(A, i, f)
9 return A[x]
```

![[Pasted image 20240821200155.png]]

Podemos parametrizar este algoritmo para obtener el k-ésimo estadístico de orden de A

### `Median` Parametrizado

```c
input: Secuencia A[0, ..., n-1]
output: k-ésimo estadistico de orden de A

Median(A, k);
1 i <- 0
2 f <- n-1
3 x <- Partition(A, i, f) // recordar que retorna el indice de un random
4 while x != k:
5	// ajuste de rango
6	if x < k : i <- x + 1
7	else: f <- x-1
8	x <- Partition(A, i, f)
9 return A[x]

// Median(A,0) entrega el menor elemento de A
// Median(A, n-1) entrega el mayor elemento de A
```

#### Complejidad de `Median`

Complejidad **probabilística**: depende de la elección del pivote

**Mejor caso**
- Escoger la mediana como primer pivote
- Implica separar los demás elementos en m y M
- Esto toma $\mathcal{O}(n)$ por pivote
	- Pero solo estamos tomando 1 pivote: Total $\mathcal{O}(n)$

**Peor caso**
- Escoger todos los datos menos la mediana como pivote
- Para cada pivote hay que separar en m y M: $\mathcal{O}(n)$
- Se toman $\mathcal{O}(n)$ pivotes
	- Total $\mathcal{O}(n^2)$


## [[Quick Sort]]

Usando `Partition` notamos lo siguiente

![[Pasted image 20240821201315.png]]

Esto nos da una idea para idear un nuevo algoritmo de ordenación

## [[Partition in-place]]

Versión *in-place* con memoria adicional $\mathcal{O}(1)$
