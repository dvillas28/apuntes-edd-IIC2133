#clase02 

Otra forma de ordenar es ir recibiendo los elementos y así ir ordenándolos a medida que vayan llegando

En lugar de ordenar desde cero, podemos **insertar** elementos respetando el orden


```c
input: Secuencia de datos A
output: Nueva secuencia de datos B, ordenada

InsertionSort(A):
1 Definir secuencia B, inicialmente vacía
2 Tomar el primer dato x de A
3 Quitar x de A
4 Insertar x en B de manera que quede ordenada
5 Si quedan datos en A, volder a la línea 2
  return B
```


**Principal diferencia con *SelectionSort*:** 
- *SelectionSort*: elegir ordenadamente (el mínimo)
- *InsertionSort*: insertar ordenadamente

## Correctitud
#### Demostración de finitud
- Sea $n$ la cantidad finita de valores en la secuencia original A
- En cada iteración del algoritmo se borra un valor (lin. 3), que luego se inserta en B
- En todo momento B tiene largo finito, por lo que la inserción toma una cantidad finita de pasos
- Luego de $n$ iteraciones, todos los valores de A fueron borrados, la linea 5 nos garantiza una condición de termino
- Por lo tanto el algoritmo termina

#### Demostración de ordenación

$P(n):=$ Luego de la $n$-ésima iteración, B esta ordenado
- CB: $P(1)$ , en la 1ra iteración, B solo tiene 1 elemento, por lo tanto esta ordenado
- HI: Suponemos que luego de la $n$-ésima iteración, B esta ordenado
- TI: En la iteración $n+1$. extraemos el primer elemento de A, a saber $a'$ . Si el estado de B es $$a_1\leq \dots \leq a_i \leq a_{i+1}\leq\dots\leq a_n$$ y $a'$ cumple que $a_1\leq a' \leq a_{i+1}$ , entonces en la $n+1$ iteración la B quedara de la siguiente forma $$a_1\leq \dots \leq a_i \leq a' \leq a_{i+1}\leq\dots\leq a_n$$ y se B se encuentra ordenada en la iteración $n+1$

## Sobre la inserción de *InsertionSort*

*InsertionSort* y *SelectionSort* no solo se diferencian en su estrategia, sino también en cómo realizan la [[Inserción de datos]] en cada iteración

- *SelectionSort* inserta siempre al final de la nueva EDD
- *InsertionSort* inserta de **forma que la nueva EDD quede ordenada** (no necesariamente al final de esta)

La inserción es $\mathcal{O}(n)$
## Complejidad

Considerar una versión in place de *InsertionSort*
- Igual que con *SelectionSort*, $|A| + |B| = n$ es un invariante
- Podemos usar el mismo arreglo

Mejor caso O(n), todas las líneas 4 toman O(1)
Caso promedio O(n^2)

#### *InsertionSort* in place

![[Pasted image 20240815185407.png]]

- comparación hacia la izquierda, por eso i parte siendo = 1
- la lista se va ordenando hacia la derecha
- linea 3, mientras el index actual sea menor al preivo, se intercambia
- Mejor caso: los datos vienen ordenados, nunca entro en el *while*, luego O(1)

#### Diferencia importante con *SelectionSort*
- *SelectionSort* revisa toda la secuencia para encontrar el elemento
- *InsertionSort* siempre toma el primer elemento de A

Si los datos vienen ordenados, *SelectionSort* no cambia su complejidad (hay que seguir recorriendo la lista)
- *InsertionSort*, la insercion es beneficiada -> es útil recordad donde termina la lista ordenada para saber donde insertar
	- **La complejidad de *InsertionSort*** depende de que tan ordenados están los datos: [[Inversiones]]

#### Complejidad de *InsertionSort* considerando inversiones

Consideremos un arreglo A de largo n, con k inversiones

- La línea que realiza los intercambios es la línea 4
- Antes de cada intercambio, se comparan los datos con índices j y j-1
	- Estos datos se intercambian solo si (j-1, j) es una inversión
- --> el intercambio de datos **adyacentes** corrige 1 inversión
- Cada dato es comparado al menos una ves con otro

De acuerdo a esto, la complejidad es $$\mathcal{O}(n+k)$$
- $n$ considera que cada dato se compara al menos una ves
- $k$ es el # de inversiones

#### Valor de $k$ en el mejor, peor y promedio

- **Mejor caso**: la lista viene ordenada, se realizan 0 inversiones
	- Complejidad: $\mathcal{O}(n)$
	
- **Peor caso**: arreglo desordenado invertido, por cada dato, se deben realizar $n$ inversiones
	- Complejidad: $\mathcal{O}(n^2)$
	- Demostración matemática ![[Pasted image 20240815192335.png]]

- **Caso promedio**: 
	- Necesitamos abstraernos del orden del arreglo
	- Considerar un arreglo A que viene en cualquier orden
		- ¿n° promedio de inversiones en un arreglo con $n$ datos?
	- Suponemos que A no tiene elementos repetidos

#### Permutación e inversiones
Dado el conjunto S con n elementos, una permutacion P de S es una secuencia que cumple
- Todos los elementos de S pertenecen a P
Para S con |S| = n, existen n! permutaciónes diferentes
- Cada una es una forma de ordenar los elementos de S
- El arreglo A corresponde a una de esas permutaciónes

Se define al numero promedio de inversiones como $$k=\frac{\sum_P{\# \text{ inv. en P}}}{\# \text{ permutaciones}}$$
**Truco**:  para una permutación P, considerar su permutación inversa P'
- Existen $\frac{n!}{2}$ pares de permutaciones acompañados de su inversa

![[Pasted image 20240815193823.png]]

- Tomando un par de elementos distintos $x, y$ de S y un par de permutaciones $P, P^r$ , los indices de $x$ e $y$ están en inversión en **alguna de las dos permutaciones** 

![[Pasted image 20240815193952.png]]

Como cada inversión aparece en una de las dos permutaciones del par P, P^r
tenemos que $$\#\text{ inv. en P} + \#\text{ inv. en P}^r = \frac{n(n-1)}{2}$$
Luego tomando, los $\frac{n!}{2}$ pares posiles de permutaciones de la forma $P_k, P_k^r$ , el promedio de inversiones es $$k=\frac{\sum_P{\# \text{ inv. en P}}}{\# \text{ permutaciones}} = \frac{\sum_{k=1}^{\frac{n!}{2}}\#\text{ inv. en P} + \#\text{ inv. en P}^r}{n!}$$
$$= \frac{\frac{n(n-1)}{2}\frac{n!}{2}}{n!}$$
$$\frac{n(n-1)}{4}$$
Una permutación promedio tiene una cantidad de inversiones: $\mathcal{O}(n^2)$

![[Pasted image 20240815194622.png]]

#### Caso promedio en algoritmos de ordenación

![[Pasted image 20240815194657.png]]


## Síntesis *InsertionSort* 

![[Pasted image 20240815194847.png]]

![[Pasted image 20240815194833.png]]

### Algoritmo in-place

```python

def InsertionSort(list A, int len) -> void:
{
	for pos_a_ordenar in range(0...len-1):
		current = i
		# if the current value is less than the previous value
		# we swap
		while (current > 0) and (A[current] < A[current - 1]):
			swap(A[current], A[current-1])
			# we move our current to the left
			current -= 1
}

# Mejor caso, no se entra en el while: O(n) (adaptativo)
# Peor caso, lista al reves, O(n^2)
# Caso promedio O(n^2)

```

Hasta ahora

![[Pasted image 20240815194907.png]]

### Uso
*InsertionSort* se usa cuando se necesita un algoritmo simple, y con un tamaño relativamente bajo (n aprox. a 100)