#clase16 

Consideremos ahora el problema de dar $S$ pesos de vuelto usando el menor número posible de monedas
- Suponemos que los valores de las monedas, ordenados de mayor a menor, son $\{v_1, v_2, \dots, v_n\}$
- Tenemos una cantidad ilimitada de monedas de cada valor

Posible estrategia con [[Algoritmos Codiciosos]]
 *Asignar tantas monedas grandes como sea posible, antes de avanzar a la siguiente moneda grande*

![[Pasted image 20241116215306.png]]

![[Pasted image 20241116215424.png]]

Dado un conjunto de valores ordenados $\{v_1, v_2, \dots, v_n\}$, definimos $z(S, n)$ como el problema de encontrar el menor número de monedas para totalizar $S$

**Ejercicio**: Proponer una recurrencia para resolver el problema $z(S, n)$ y plantear un algoritmo a partir de ella

Sea $Z(S,n)$ la solución óptima al problema $z(S,n)$. Para buscar intuición, notamos que hay dos opciones respecto a las monedas de valor $v_n$

- Si se incluye una moneda de valor $v_n$ $$Z(S, n) = Z(S-v_n, n) + 1$$
- Si no se usan monedas de valor $v_n$ $$Z(S,n) = Z(S, n-1)$$ $n-1$ ya que no consideramos las monedas de valor $v_n$

Luego generalizamos la idea

- Para las monedas de valor $v_n$ $$Z(S,n) = min\{Z(S-v_n, n) + 1, Z(S, n-1)\}$$
- Luego generalizamos para el subconjunto de los primeros $k$ valores de monedas $$Z(T,k) = min\{Z(T-v_k, k) + 1, Z(S, k-1)\}$$ donde $Z(T,0) = +\infty$ si $T>0$ y $Z(0,k) = 0$

Con esto, podemos plantear el siguiente algoritmo recursivo

```c

Change(S):
	for T = 1,...,S: // Loop de seteo
		Z[T][0] <- +inf
	for k = 0,...,n:
		Z[0][k] <- 0
	for k = 1,...,n:
		for T = 1,...,S:
			Z[T][k] <- Z[T][k-1]
			if T - v_k >= 0:
				Z[T][k] <- min{Z[T][k-1], Z[T-v_k][k]+1}

```


