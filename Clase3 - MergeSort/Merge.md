#clase03 
Ejemplo visto en clases, la secuencia parcialmente ordenada

![[Pasted image 20240819191307.png]]

Sea i el indice de la posicion, si queremos ordenarla usando InsertionSort tenemos que
- Hasta i = 9, la ordenación es $\mathcal{O}(n)$ (la 1° sub-lista esta ordenada)
- Desde i=10, la ordenación es $\mathcal{O}(n^2)$ (hay que ir insertando los elementos de la 2° sub-lista en la 1°)

Teniendo una lista parcialmente ordenada con dos sub-listas, **existe una mejor estrategia**
**para obtener una lista ordenada, aprovechando el orden**

## El algoritmo ``Merge``

```c
input: Secuencias ordenadas A y B
output: Nueva secuencia ordenada C

Merge(A, B):
1 Iniciar C vacía
2 Sea a y b los 1°ros elementos de A y B
3 Extraer el menor entre a y b
4 Insertar ese elemento al final de C
5 Si quedan elementos en A y B, volver a línea 2
6 Concatenar C con la secuencia que aun tenga elementos (sigue ordenada)
  return C
```

## Correctitud
### Demostración (finitud)

En cada iteración del algoritmo, se va extrayendo un elemento de alguna de las dos secuencias
- linea 5 es la que verifica si se hay una secuencia se haya quedado sin elementos
Una vez una de ellas se queda sin elementos, se insertan los elementos de la otra directamente en C (concatenación de la línea 6)
- En total se realizan $n = |A|  + |B|$ inserciones y un numero de comparaciones <= $n$ , luego el algoritmo termina en una cantidad finita de pasos

### Demostración (cumple el proposito)

Para A, B inicialmente ordenadas, considerar

$P(n):=$ Luego de insertar el $n$-esimo elemento en C, A, B y C están ordenadas
- CB: P(1)
	- Quitamos el primer elemento de A, sigue ordenada
	- Quitamos el primer elemento de B, sigue ordenada
	- Al colocar cualquiera de los 2 en C, C tiene un solo elemento, luego esta ordenada
- HI: Suponemos que luego de insertar el $n$-esimo elemento en C, A, B y C están ordenadas
- TI: Consideramos ahora la iteración $n+1$
	- Tenemos dos casos
		1. Aun quedan elementos en A y en B, sea $c_{n+1}$ el mínimo entre los primeros elementos de A y B (esto es, a y b)
			- Como ambas secuencias de origen se encuentran ordenadas, al quitar su primer elementos, siguen estándolo (A y B están ordenadas)
			- Sin perdida de generalidad, suponemos que $c_{n+1} \in$ A , 
			- $c_{n+1}$ cumple que es mayor que todos los elementos actuales que están en C. C tiene $n$ elementos, por HI, esta ordenado
			- por lo tanto, al agregarlo al final, C sigue ordenado (ahora con $n+1$ elementos)
				- Si lo anterior no se cumpliera entonces se implican una de las siguientes contradicciones
					- A o B no están ordenadas (demostrado que si lo están)
					-  $c_{n+1}$ fue extraído en una iteración anterior por el criterio de selección 
			- Por lo tanto se concluye que C esta ordenado


## Complejidad de memoria

Estamos considerando una implementación donde de depositan los valores a una nueva secuencia C, donde necesitamos memoria adicional
- Necesitamos memoria adicional $\mathcal{O}(n)$
	- Nos libera de mover elementos dentro las secuencias

Pero tenemos que $|A|+|B| = n$ 
- Podemos realizar `Merge` *in place*
	- Usar el mismo espacio reservado a A y B, memoria adicional $\mathcal{O}(1)$
		- Esto impacta en la complejidad de tiempo

### Complejidad considerando la implementación sugerida

El algoritmo presenta 2 fases
1. Extracción de ambas secuencias A y B
		- Decisión de quien extraer comparando: $\mathcal{O}(1)$
		- Inserción del dato en C: $\mathcal{O}(1)$
		- Lo anterior se repite $\mathcal{O}(n)$ veces
	- Total :$\mathcal{O}(n)$
2. Reubicación de la secuencia no vacía que resta
		- Tomar un elemento de la restante: $\mathcal{O}(1)$
		- Inserción del dato en C: $\mathcal{O}(1)$
		- Lo anterior se repite $\mathcal{O}(n)$ veces
	- Total: $\mathcal{O}(n)$

**Usando $\mathcal{O}(n)$ memoria adicional, `Merge` es $\mathcal{O}(n)$**

### Complejidad considerando el mismo espacio
El algoritmo presenta 2 fases
1. Extracción de ambas secuencias A y B
		- Decisión de quien extraer comparando: $\mathcal{O}(1)$
		- Inserción del dato al comienzo $\mathcal{O}(n)$
		- Lo anterior se repite $\mathcal{O}(n)$ veces
	- Total : $\mathcal{O}(n^2)$
2. Reubicación de la secuencia no vacía que resta: **NO es necesario**
		- El resto de los elementos esta en la posición correcta

**Usando $\mathcal{O}(1)$ memoria adicional, `Merge` es $\mathcal{O}(n^2)$**