#clase14

![[Pasted image 20241109215527.png]]

#### a) Identificar Variables, Dominios y Restricciones del problema

Denotaremos por $w_i$ y $l_i$ el peso y largo del auto $i$-ésimo

- Variables $X = \{x_1, \dots, x_n\}$, una para cada auto indicando si se sube o no a la barcaza
- Dominios idénticos para cada variable: $\{0,1\}$, donde 1 indica que sí se sube
- Restricciones
	- Peso máximo: W = `B.max_carga` tal que $$\sum_{i=1}^nx_iw_i \leq W$$
	- Largo máximo: L =(`B.n_filas`)(`B.m_por_fila`) tal que $$\sum_{i=1}^nx_il_i\leq L$$

#### b)
![[Pasted image 20241109215619.png]]

![[Pasted image 20241109222618.png]]

![[Pasted image 20241109222625.png]]
