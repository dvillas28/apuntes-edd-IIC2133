#clase15 

Consideremos el problema de escoger tareas

- La tarea $i$ tiene un plazo $d_i$ (día del mes)
- Además tiene una ganancia $p_i$ que se obtiene si la tarea se hace a tiempo (antes del plazo)

Una tarea toma **un día en completarse** y solo puede realizar **una tarea al día**

**Objetivo: maximizar la ganancia total**

Una solución factible será un subconjunto $T$ de tareas que se pueden realizar en algún orden

- El **valor** de $T$ será $$p(T) = \sum_{k \in T}p_k$$ Una solución factible $T$ es óptima si su valor $p(T)$ es máximo
	- Queremos hacer la máxima cantidad de tareas a tiempo

![[Pasted image 20241109234212.png]]

![[Pasted image 20241109234237.png]]


