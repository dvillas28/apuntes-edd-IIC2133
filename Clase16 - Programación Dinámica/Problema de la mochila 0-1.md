#clase16 

Consideremos el problema de la mochila con $n$ objetos **no fraccionables** (cada uno se incluye o no se incluye)

- El objeto $k$ tiene un valor $v_k$ y un peso $w_k$
- La mochila tiene capacidad de peso $W$ tal que $$W < \sum_k w_k$$
El **objetivo** es maximizar la suma de valores incluidos

## Modelamiento del problema

Usaremos la variable $x_k \in  \{0,1\}$ para indicar si el objeto $k$ se incluye o no. Resolveremos este problema con programación dinámica

Denotamos por $knap(p, q, \omega)$ al problema $$max \sum_{k=p}^q v_kx_k$$
sujeto a $$\sum_{k=p}^q w_k x_k \leq \omega$$
$$x_k \in \{0,1\}$$

Nuestro problema a resolver es $knap(1, n, W)$

## Analisis de casos

Sea $\Omega = y_1, y_2, \dots, y_n$ una elección óptima de valores binarios para las variables $x_1, x_2, \dots, x_n$

En particular $y_1$ tiene dos opciones

- Si $y_1 = 0$, entonces el objeto 1 no está en la solución. Luego $y_2, \dots, y_n$ debe ser solución óptima para $$knap(2, n, W)$$ De lo contario $y_2, \dots, y_n$ no sería solución óptima de $knap(1,n,W)$

- Si $y_1 = 1$, entonces $y_2, \dots, y_n$ debe ser solución óptima para $$knap(2,n,W-w_1)$$ De lo contrario, habría otra selección $z_2, \dots, z_n$ binaria tal que $$\sum_{k=2}^bw_kz_k \leq W-w_1$$ y $$\sum_{k=2}^q w_k z_k > \sum_{k=2}^q w_k y_k$$ por lo que $y_1, z_2, \dots, z_n$ sería una elección mejor para $knap(1,n,W)$. Esto contradice que $y_1, y_2, \dots, y_n$ es óptima

## Estrategia recursiva de sub-problemas

Sea $g_k(\omega)$ el valor de una solución óptima para $knap(k+1, n, \omega)$
- $g_0(W)$ es el valor óptimo de $knap(1,n,W)$

- Como hay decisión binaria para $x_1$, $$g_0(W) = max\{g_1(W), g_1(W-w_1) + v_1\}$$
- Podemos generalizar para un $0 \leq k \leq n$ $$g_k(\omega) = max\{g_{k+1}(\omega), g_{k+1}(\omega - w_1) + v_{k+1}\}$$ donde 
$$g_n(\omega) = \begin{cases} 
      0 & \omega \geq 0 \\
      -\infty & \omega < 0 
   \end{cases}$$

![[Pasted image 20241116214756.png]]

