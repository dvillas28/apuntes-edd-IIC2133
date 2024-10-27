#clase04 #clase05

Nuevamente usamos la estrategia [[Dividir para conquistar]], para ordenar elementos

```c
input: Secuencia A[0, ..., n-1], indices i, f
output: null

QuickSort(A, i, f): // Tambien llamado PartitionSort
1 if i <= f:
2     p <- Partition(A, i, f)
3     QuickSort(A, i, p-1) // particionar la primera mitad
4     QuickSort(A, p+1, f) // particionar la segunda mitas
```

El llamado inicial es `QuickSort(A, 0, n-1)`
## Ejemplos de ejecución

![[Pasted image 20240821201847.png]]


## Complejidad de memoria

- `QuickSort` solo depende de `Partition`
	- Tenemos una version $\mathcal{O}(n)$ de `Partition`

Contamos con una versión *in-place* de `Partition` ([[Partition in-place]])
- El algoritmo termina y es correcto
- Usaremos arreglos
- Se hacen intercambios dentro de este
- TRUCO: colocar el pivote al final

## Correctitud

### Demostración (Terminación)

Nos afirmamos del hecho de que `Partition` termina
- Por lo que la línea 2 toma una cantidad finita de pasos

Luego para ambos llamados de `QuickSort` se esta reduciendo el rango
- Tamaño de la instancia analizada `d = f - i`
- Por lo tanto en algún momento la condición de la línea 1 dejara de ser verdadera y el algoritmo terminada 
	- Si `d<0`, `QuickSort` termina sin hacer mas llamados recursivos (línea 1)
	- Si `d>= 0`, se hacen dos llamados recursivos con un rango mas pequeño
		- `d1 = p - 1 - i` y `d2 = f - p - 1`
		- En ambos llamados el rango `d` disminuye al menos en 1 de ambos llamados
	- En ambos casos, tenemos que en una recursión, cualquiera de los dos llamados reduce en 1 el rango, luego se llega a un tamaño 0, donde el algoritmo termina con las recursiones
	- Como el llamado inicial de `QuickSort(A, 0, n-1)`, la profundidad máxima de recursión es `n-1` y por lo tanto el algoritmo termina
### Demostración (Correctitud)

Nos afirmamos del hecho de que `Partition` es correcto para un pivote
Para demostrar que `QuickSort` ordena, tenemos que demostrar todos los elementos serán pivotes en algún momento de la ejecución del algoritmo

PD: Todo elemento de `A[0...n-1]` es elegido como pivote en algún llamado de ``Quicksort``

Antes que nada, `QuickSort` verifica si hay elementos en el rango `i...f`
- Si `i > f`: no quedan elementos que puedan ser escogidos como pivote
- Si `i <= f` el rango de posibles pivotes a seleccionar es `d = f - 1 > 0`
	- Se escogen 2 pivotes de ese rango y se crean dos nuevos rangos cuya suma es `f - i - 1`
	- Dado que en cada llamado no vacío se escoge un pivote, los llamados siempre reducen su tamaño y el algoritmo solo detiene las recursiones cuando el llamado es vacío, por lo que todo elemento es escogido como pivote en algún llamado. 
- Como `Partition` es correcto, todo elemento queda ordenado
## Complejidad de tiempo

La complejidad depende de la elección del pivote: es **probabilística**

- **Mejor Caso**: Llamadas recursivas con subsecuencias del mismo tamaño
	- Esto ocurre cuando siempre se elije como pivote, al elemento que va justo en medio, en cada recursión (azar)
	- Llamadas recursión izq. = llamadas recursión derecha (llamadas balanceadas)
		- Esto se visualiza como un triangulo invertido
	- Se genera una ecuación de recurrencia $$T(n) = n + 2T(\frac{n}{2})$$ como en `MergeSort`
		- Que demostramos tiene una complejidad $\mathcal{O}(n\log n)$
	
	![[Pasted image 20240826190324.png]]

- **Peor Caso:** ``Partition`` genera sub-secuencias de tamaño 0 y n-1
	- n divisiones
	- Se genera una ecuación de recurrencia $$T(n) = n + T(n-1)$$ donde $n$ es el llamado de `Partition` ($\mathcal{O}(n)$) y $T(n-1)$ es el llamado recursivo de ``QuickSort`` a la subsecuencia de tamaño $n-1$
	- Esto resulta en una complejidad resultante de $\mathcal{O}(n^2)$

![[Pasted image 20240826190336.png]]

***OBS***: El peor caso de ``QuickSort`` depende como implementamos ``QuickSort``
- Referido a la elección del pivote
	- Si tomamos como pivote siempre el primer elemento y la lista esta ordenada
		- Se tienen subsecuencias de tamaño 0 y n-1

#### Caso promedio

![[Pasted image 20240826190353.png]]
![[Pasted image 20240826190401.png]]
![[Pasted image 20240826190427.png]]
## Uso típico y mejoras de `QuickSort`

- ``QuickSort`` es un excelente algoritmo para uso general
- No requiere memoria adicional

- Sobre costo de la recursión
	- Muchos datos, se comporta bien, pero el costo de la recursión es alto
	- Entra en factor, el código, el compilador, el SO, sobre como se gestionan las recursiones (pueden ser secuenciales en profundidad o en paralelo)

- Para subsecuencias pequeñas (n <= 20), podemos usar `InsertionSort`
	- A pesar de tener una complejidad peor asintóticamente, en instancias pequeñas tiene mejor rendimiento que `QuickSort`

- Mejora: Usar la mediana de 3 elementos como pivote
	- Informar la elección de pivote
	- Dado `A` escogemos `A[k1], A[k2], A[k3]`
	- En $\mathcal{O}(1)$ encontramos la mediana entre ellos
	- En una medida anti envenenamiento
		- La idea es nunca caer en los bordes

- Particionar la secuencia en 3 sub-secuencias
	- Mejora para el caso con datos repetidos (duplicados)
	- Evita que `Partition` particione innecesariamente sub-secuencias en que todos los valores sean iguales

## Síntesis hasta ahora

![[Pasted image 20240826190826.png]]