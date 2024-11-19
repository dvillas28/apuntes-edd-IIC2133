#clase15

Los **algoritmos codiciosos** plantean una estrategia algorítmica basada en el paradigma de subconjuntos

1. Tenemos un conjunto $\mathcal{S} = \{s_1, \dots, s_n\}$ con $n$ inputs
2. Queremos un subconjunto $\mathcal{S}' \subseteq \mathcal{S}$ que satisfaga restricciones
3. Queremos una solución factible que maximice o minimice una **función objetivo**

Un subconjunto $\mathcal{S}'$ que cumple las restricciones se llama **factible**. Una solución que maximiza/minimiza se llama **óptima**

Los **algoritmos codiciosos** trabajan en etapas
- Consideran un input a la vez
- Una vez que se decide sobre un input, la decisión es **final**
- Ninguna decisión posterior cambia la actual

En el caso del problema de la mochila
- Se trata de seleccionar un subconjunto de objetos y determinar la fracción $x_k$

Para lograr este objetivo, debemos considerar los input en cierto orden
- Se usa un **procedimiento de selección**
- Si la inclusión del próximo input en la solución óptima parcial produce solución infactible, no lo consideramos
- En otro caso, el input se agrega a la solución

Este procedimiento de selección se basa en una **medida de optimización** o **estrategia codiciosa**
- Se selecciona un input de forma **localmente óptima**
- Esperamos que esa selección nos lleve a una solución globalmente óptima

![[Pasted image 20241109231134.png]]

Normalmente, la mayoría de las estrategias no producen soluciones óptimas

![[Pasted image 20241109231156.png]]

En este problema, el óptimo se encuentra privilegiando ganancia/peso

Dado un problema
- Varias estrategias codiciosas pueden ser plausibles
- La mayoría produce soluciones **subóptimas**

Para garantizar que una estrategia produce soluciones óptimas es necesario **demostrarlo** (en este curso no nos preocuparemos de este último aspecto)

## Idea de pseudocódigo

```c
input: Array de inputs A[0...n-1], cantidad de inputs n 

Greedy(A, n):
1 S <- null
2 for i in 1...n
3     x <- Select(A)
4     if Feasible(S, x):
5         S <- Union(S, x)
6 return S
```

## 2 aplicaciones

1. [[Problema de asignar charlas]]
2. [[Problema de escoger tareas]]
