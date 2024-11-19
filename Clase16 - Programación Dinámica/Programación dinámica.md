#clase16 


## Caso de motivación

Considerar nuevamente el problema de asignar charlas en una misma sala

- Tenemos $n$ charlas por asignar
- La charla $i$ tiene hora de inicio $s_i$ y de término $f_i$
	- Es decir, se define el intervalo de tiempo $[s_i,f_i)$
- Solo se puede realizar **una charla a la vez**

Además, si la charla $i$ es realizada, se produce una ganancia $v_i$

Objetivo: maximizar la ganancia

![[Pasted image 20241116204107.png]]

### Caso con $v_i = c, \forall i$

Esto es greedy, visto en [[Problema de asignar charlas]]

### Caso con ganancias diferentes

![[Pasted image 20241116204224.png]]

![[Pasted image 20241116204235.png]]


## Programación Dinámica

Nueva estrategia: programación dinámica

- Generalmente usada en problemas de optimización
- Se basa en la existencia de **subproblemas** que permiten resolver el problema original
- Además los problemas se **solapan**. I.e. comparten **sub-subproblemas**

[[Dividir para conquistar]]: Sub-problemas disjuntos, en Programación Dinámica ya no lo son

La clave de programación dinámica es **recordar las soluciones a los sub-problemas**

## Programación de charlas 2.0

![[Pasted image 20241116204819.png]]

Consideremos una instancia de charlas $\{1, \dots, n\}$ ordenadas por $f_i$. Supongamos que tenemos una solución óptima $\Omega$ para este problema

Consideremos la última charla, i.e. $n$. Tenemos dos opciones.

1. Si $n \notin \Omega$, entonces $\Omega$ es solución del **sub-problema** que solo considera las charlas $\{1, \dots, n-1\}$
2. Si $n \in \Omega$, entonces no hay charla $r$ tal que $b(r) < r < n$ que esté en $\Omega$. Además, $\Omega$ contiene una solución optima al **sub-problema** con charlas $\{1, \dots, b(n)\}$

Para encontrar la solución a un problema, necesitamos las soluciones a los problemas más pequeños

Formalizando las ideas anteriores

- Sea $\Omega_j$ la solución al problema con charlas $\{1, \dots, j\}$ y sea $opt(j)$ su ganancia total. **Objetivo final:  Obtener $\Omega_n$ con valor $opt(n)$
- Para cada $1 \leq j \leq n$, hay dos casos
	- Si $j \in \Omega_j$, entonces $opt(j) = v_j + opt(b(j))$
	- Si $j \notin \Omega_j$, entonces $opt(j) = opt(j-1)$
- Para saber si $j \in \Omega_j$, comparamos las dos opciones $$opt(j) = max\{v_j + opt(b(j)), opt(j-1)\}$$
La ecuación anterior permite plantear el siguiente algoritmo recursivo

```c
input: natural 0 <= j <= n
output: ganancia óptima

Opt(j):
1     if j = 0
2         return 0
3     else:
4         return max{v_j + Opt(b(j)), Opt(j-1)}

// Notamos que Opt requiere
// - Tener ordenadas las charlas por hora de termino y conocer b(j)
// - suponer que Opt(0)

```

Este algoritmo tiene un gran problema: su complejidad, es $\mathcal{O}(2^n)$

![[Pasted image 20241116210115.png]]

A pesar de hacer una cantidad exponencial de llamadas, realmente se resuelven solo $n+1$ sub-problemas $$Opt(0), Opt(1), \dots, Opt(n)$$
Es este problema, un mismo llamado puede aparecer varias veces en el árbol de recursión. ¿Podríamos hacerlo mejor?

**FIX**: Agregaremos un arreglo global $M$ donde almacenaremos cada `Opt(j)` la primera vez que lo calculamos

```c

RecOpt(j)
1     if j = 0:
2         return 0
3     else:
4         if M[j] != null: // si ya tenemos el resultado calculado
5             return M[j] 
6         else: // si no, lo calculamos 
7             M[j] <- max{v_j + Opt(b(j)), Opt(j-1)}
8             return M[j]

```

El algoritmo `RecOpt` toma tiempo $\mathcal{O}(n)$

![[Pasted image 20241116210549.png]]

![[Pasted image 20241116210556.png]]

### Solución Iterativa

También podemos plantear una solución iterativa para el problema, computando los sub-problemas en orden de tamaño

```c
ItOpt():
1     M[0] <- 0
2     for j in 1, ..., n:
3         M[j] <- max{v_j + Opt(b(j)), Opt(j-1)}
```

Al terminar, `ItOpt` deja en $M$ las ganancias óptimas, y el algoritmo también toma tiempo $\mathcal{O}(n)$

## Planteamiento de la estrategia

Planteamos la estrategia de **programación dinámica** para resolver un problema:

1. El número de sub-problemas es (idealmente) polinomial

2. La solución al problema original puede calcularse a partir de sub-soluciones

3. Hay un **orden natural** de los sub-problemas. (*del mas pequeño al mas grande*) y una recurrencia sencilla (*la ecuación*)

4. Recordamos las soluciones a sub-problemas

La recurrencia es la clave para plantear el algoritmo base 

## Dos aplicaciones

1. [[Problema de la mochila 0-1]]
2. [[Problema de dar vuelto]]