#clase07 

- Un algoritmo algo mas general
- Permite ordenar cosas mas generales (patentes, nombres, alfabetos, *etc*)

## Historia del algoritmo

- Usado por las máquinas que ordenaban tarjetas
	- Cada tarjeta tiene 80 columnas y 12 líneas
	- Cada columna puede tener un agujero en una línea

- `RadixSort` ordena las tarjetas revisando una columna determinada
	- Si hay un agujero en la columna, se pone en uno de los 12 compartimientos
	- Las tarjetas con la perforación en la primera columna quedan encima
	- Esta idea funciona para $d$ columnas

Podemos generalizar esto para un **número natural de $d$ dígitos**

## Ordenando por dígito

Considerar un número natural de $d$ dígitos $n_{0}n_{1}\dots n_{d-1}$
- Podemos ordenar según el dígito más significativo $n_{0}$
	- Según este dígito, separamos los números en *compartimientos
	- Luego, ordenamos recursivamente cada compartimiento por el segundo digito más significativo $n_{1}$
- Finalmente se combinan los contenidos de cada compartimiento

Esto presenta un problema -> muchos llamados recursivos

Un ingrediente fundamental para el algoritmo que se plantea es que este sea un [[Algoritmo Estable]]

## `RadixSort`

`RadixSort` ordena por dígito **menos significativo**
- Ordena por dígito $n_{d-1}$
- Luego, usando el mismo arreglo, se ordena por dígito $n_{d-2}$, **con un algoritmo estable**
- Luego de ordenar `k` dígitos, los datos están ordenados **si solo miramos el fragmento** $n_{d-k}\dots n_{d-1}$ 
- Requerimos de `d` pasadas para ordenar la secuencia completa

```c
RadixSort(A, d):
	for j = 0...d-1:
		StableSort(A, j) // algoritmo de ordenación estable por j-esimo dígito menos significativo
```

### Ejemplo de ejecución

![[Pasted image 20240908185759.png]]

## Complejidad

Supongamos que `A` tiene $n$ datos naturales con $d$ dígitos y se usa un algoritmo estable **lineal**
- Si cada digito puede tomar $k$ valores distintos
	- Entonces `RadixSort` toma tiempo $\Theta(d(n+k))$
	- Si $d$ es constante y $k \in \Theta(n)$, entonces toma tiempo $\Theta(n)$

## Implementación

### LSD *string sort* (*Least Significant Digit*)

- Si todos los *strings* son del mismo largo
	- patentes, IP's, telefonos
- Funciona bien si el largo es pequeño
- No es recursivo

### MSD *string sort* (*Most Significant Digit*)

- Si los *strings* tienen largo diferente
- Ordenamos con `CountingSort()` por 1° carácter
- Recursivamente ordenamos sub-arreglos correspondientes a cada carácter (excluyendo el primero, que es común en cada sub-arreglo)
- Como `QuickSort`, puede ordenar en forma independiente (usar varios núcleos de la CPU)
	- **Pero** particiona en tantos grupo como valores del primer carácter

#### ejemplo de ejecución

![[Pasted image 20240908191424.png]]

#### Cuidados de MSD

En MSD debemos considerar

- Si un *string* $s_1$ es prefijo de otro $s_2$ -> $s_1$ es menor que $s_2$
	- `she` $\leq$ `shells`
- Pueden usarse diferentes alfabetos
	- Binario (2)
	- minúsculas (26)
	- minúsculas + maýusculas + dígitos (64)
	- ASCII (128)
	- Unicode (65.536)
- Para subarreglos pequeños (`|A| <= 10`)
	- podemos cambiar a `InsertionSort` que sepa que los primeros `k` caracteres son iguales