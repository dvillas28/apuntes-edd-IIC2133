#clase01 

### Secuencias ordenadas
Si yo *etiqueto* las cosas, las puedo ordenar
#### Definición

![[Pasted image 20240806223033.png]]

#### Propuesta de algoritmo de ordenación
````
input: Lista de nombres L
output: Lista ordenada de nombres L'

Misterio(L):
1 Iniciar L' vacía
2 Encontrar el menor valor en L
3 Borrar el valor encontrado
4 Escribirlo al final de L' (en el primer espacio disponible)
5 Si quedan valores en L, volver a la línea 2
  return L'
````

Este algoritmo `Misterio` se conoce como [[Selection Sort]]

Queremos saber si este algoritmo es **correcto**, es decir
- Termina en una cantidad finita de pasos
- Cumple su propósito

En este problema de ordenación, un algoritmo será correcto si **ordena** los datos en una cantidad finita de pasos

Para demostrar esto, podemos usar [[Inducción simple]]

### Ejemplo

Queremos demostrar que `Misterio` es correcto

#### Demostración: finitud

Sea $n$ la cantidad (finita) de valores en la lista original `L`

En cada iteración del algoritmo se borra un valor de `L` y se escribe en la lista nueva `L'`.

Luego de $n$ iteraciones, todos los valores de `L` fueron borrados. Debido a la la línea 5, que verifica si existen valores en `L` el algoritmo no sigue iterando,

Por lo tanto el algoritmo termina en una cantidad finita de pasos

#### Demostración: 

Demostraremos por inducción que efectivamente se genera una lista ordenada
- Propiedad $P(n)$ := Los primeros $n$ valores borrados de `L` son los menores de `L` y están ordenados en `L'`.

1. CB. $P(1)$ . A `L` le fue borrado su menor elemento (criterio de la línea 2). Dado que `L'` solo tiene 1 elemento ($a_1$) `L'` esta ordenada
2. HI. Suponemos que los primeros $n$ valores borrados de `L` son los menores y se encuentran ordenados en `L'`
- P.D: primeros $n+1$ valores borrados de `L` son los menores y se encuentran ordenados en `L'`
Por HI, los primeros $n$ elementos son los $n$ menores elementos de `L` y están ordenados en `L'`. Podemos asignarles etiquetas a todos estos elementos

	$a_1 \leq a_2 \leq ... \leq a_n \leq$ cualquier elemento restante en  ``L`` 

Al borrar el elemento $n+1$ de `L`, lo llamamos $a_{n+1}$ por criterio de la línea 2 sabemos que este es menor que todos los elementos que restan en `L`

Por HI sabemos que 
	$a_1 \leq a_2 \leq ... \leq a_n \leq a_{n+1} \leq$ cualquier elemento restante en ``L`` 

Y `L'` sigue ordenada de forma no decreciente con $n+1$ elementos

Con esto se concluye que el algoritmo ordena


## *Tips* para demostrar correctitud

- Terminación
	- revisar la condición de termino (una línea)
	- Casos donde se podría quedar pegado y argumentarlos
- Correctitud
	- Lo complicado es escoger una proposición
	- De que forma cuando estamos en la mitad del trabajo, sabemos que estamos bien -> proposición
	- De que manera sabemos que el algoritmo va funcionando, cuando estamos en la mitad de la ejecución de varias iteraciones de este