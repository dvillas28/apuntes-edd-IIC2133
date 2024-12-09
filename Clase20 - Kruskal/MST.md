#clase20 

## Definición

Dado un [[Grafo]] no dirigido $G$, un sub-grafo $T \subseteq G$ se dice **árbol de cobertura mínimo** o **MST** de $G$ si
1. $T$ es un árbol
2. $V(T) = V(G)$
3. No existe otro MST $T'$ para $G$ con menor costo total

i.e, si $T$ es MST de $G$
1. no tiene ciclos
2. es una **cobertura** de los nodos de $G$
3. tiene costo minimo

Árboles de coberturas mínimos

![[Pasted image 20241120122618.png]]
![[Pasted image 20241120122622.png]]

Los MST están presentes en la solución de múltiples problemas de conectividad
- Redes de distribución eléctrica
- Redes telefónicas
- Comunicaciones, computacionales, tráfico aéreo...
- Incluso en redes biológicas, químicas y físicas

Para atacar el problema algorítmicamente, dado $G$ no dirigido

- Llamamos **corte** a una **partición** $(V_1, V_2)$ de $V_G$ $$V_1, V_2 \neq \emptyset$$ $$V_1 \cup V_2 = V_G$$ $$V_1 \cap V_2 = \emptyset$$
- Diremos que una arista **cruza el corte** si uno de sus extremos está en $V_1$ y el otro en $V_2$ (une dos particiones)


Si $T$ es un MST de $G$, y $P=(V_1, V_2)$ es un corte de $G$
- Sabemos que al menos una arista que cruza $P$ está incluida en $T$
	- De lo contrario, no habría camino entre nodos de $V_1$ y $V_2$ y por lo tanto $T$ no sería de cobertura

Si $P=(V_1, V_2)$ es un corte de $G$
- Sabemos que cada arista de corte tiene un costo asociado
- La arista más barata **siempre** se incluye en **algún MST**

Usaremos estas ideas para construir un MST desde cero, con dos algoritmos distintos
- [[Algoritmo de Kruskal]]
- [[Algoritmo de Prim]]