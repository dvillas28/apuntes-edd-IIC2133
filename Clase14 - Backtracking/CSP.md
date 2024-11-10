#clase14 
## Definición

Un problema de satisfacción de restricciones o *constraint satisfaction problem* (CPS) es una tripleta $(X,D,C)$ tal que

- $X = \{x_1,\dots, x_n\}$  es un conjunto de **variables**
- $D = \{D_1,\dots, D_n\}$  es un conjunto de **dominios** respectivos **para cada variable**
- $C = \{C_1,\dots, C_m\}$  es un conjunto de **restricciones**

donde cada restricción involucra a un subconjunto de variables de $X$. Una **solución** es una asignación de las variables en sus dominios tal que se satisfacen todas las restricciones.

- No necesariamente las variables son del mismo dominio
- Una restricción $C_j$ puede involucrar 1, 2 o más variables de $X$


## Ejemplos de CSPs

### Problema de las 8 reinas

#### Planteamiento inicial

![[Pasted image 20241109200338.png]]

#### Reescrito como CSP

- Variables
	- $X = \{x_1,\dots,x_8\}$ 
	- Cada variable $x_i$ se interpreta como columna de la reina en la fila $i$
- Dominios
	- $D = \{B,\dots,B\}$ con $B = \{1,\dots,8\}$
	- En este caso, el dominio de cada variable en $X$ es el mismo
- Restricciones
	- **Dos reinas no deben estar en la misma fila**: Las restricción sobre las filas esta implícita en la elección de las variables
	- **Dos reinas no deben estar en la misma columna**:  $$i \neq j \implies x_i\neq x_j$$
	- **Dos reinas no deben estar en un camino diagonal**: $$i\neq j \implies |\frac{(x_j-x_i)}{j-i}| = 1$$



## Resolución de CSPs

¿Qué tan rápido pueden resolverse los problemas CSP?

Podemos considerar un problema central en computación. Los [[SAT]]

Ahora, para $\varphi \in \mathcal{L}(P)$ podemos interpretar la pregunta "¿$\varphi$ es satisfacible?" como un CSP donde

- $X = P$, un conjunto de variables proposicionales
- $D = \{B, \dots, B\}$ con $B=\{0,1\}$
- Restricciones de que el valor de verdad de $\varphi$ sea 1 al evaluar los valores asignados a cada variable.

Si tuviéramos una forma eficiente de resolver un **CSP**, podríamos usarla para resolver un **SAT**

**Teorema**: el problema de decisión **SAT** es **NP-completo**

Los problemas NP-completos son considerados difíciles
- Es un problema abierto saber si se pueden resolver problemas de manera eficiente
- Además, todo problema NP-completo sirve para resolver otro problema NP-completo

Con esto, los CSP servirían para resolver cualquier problema NP-completo
- Conclusión: los CSP son difíciles

### Una opción: [[Fuerza Bruta]]

![[Pasted image 20241109202611.png]]

### Otra opción: *[[Backtracking]]*

#### Ejemplo con el problema de las 8 

Aplicamos la estrategia de *backtracking* a este problema. Queremos ver si una asignación parcial de las 8 reinas puede dar lugar a una solución válida


```c
input: Array T[0...7], indice 0 <= i <= 8
output: true si y solo si hay solucion

// notar que se aplica la estrucura general del backtracking

Queens(T, i):
1 if i = 8: return true
2 for v in 0...7:
3     if Check(T, i, v): // la asignacion no rompe las restricciones
4         T[i] <- v
5         if Queens(T, i+1):
6             return true
7 return false
```

```c
input: Array T[0...7], indices 0 <= i <= 7
output: false si y solo si la asignacion es ilegal

Check(T, i, v):
1 for j in 0...i-1:
2    if v = T[i]:             // restriccion de columnas
3        return false
4    if |(v-T[j])/(i-j)| = 1: // restriccion de diagonal
5        return false
6 return true
```

### Complejidad Fuerza bruta vs *Backtracking*

![[Pasted image 20241109205843.png]]

