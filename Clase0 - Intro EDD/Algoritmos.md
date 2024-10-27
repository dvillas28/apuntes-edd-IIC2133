#clase00 
## Definición

Secuencia ordenada de pasos que permite hacer un calculo o hallar la solución de un tipo de problemas

Los algoritmos son independientes de los lenguajes de programación

Puede estar dado/descrito por cualquier lenguaje
- Lenguaje de programación
	- [[C]], Python, Java, C++, etc.
- Lenguaje natural
	- Depende del contexto
	- es ambiguo
- [[Seudocódigo]]

Para un algoritmo no existe una única **implementación**
- Clases: algoritmos de manera conceptual
- Tareas: pensar como implementarlos

No solo nos interesa que la implementación sea **correcta** ([[Correctitud de algoritmos]]), también nos interesa saber **qué tan buena** es una solución a un problema. 

La principal herramienta que usaremos para esto es la [[Complejidad Computacional]]

### Complejidad: resumen de cálculo

Nos interesan dos tipos de complejidades para algoritmos como funciones del **tamaño del input** n (i.e. # de datos de entrada)
- Complejidad de tiempo $T(n)$
- Complejidad de memoria **adicional**: $M(n)$
	- Si por ejemplo necesitamos duplicar un arreglo

Si bien en general $T(n)$ es nuestra prioridad, no hay que  olvidar que:
$$T \in \Omega(M)$$
#### Etapas dentro de un algoritmo

Etapas sucesivas (una después de otra)

- La complejidad de la secuencia de etapas es la **suma** de sus complejidades
- **Consecuencia**: un paso que se repite $n$ veces, en general, contribuye con una complejidad que es $n$ **veces** la complejidad del paso individual
	- Ejemplo: ``for`` dentro de otro ``for`` (Complejidad $\mathcal{O}(n^2)$)
- Al sumar, el término que **crece más rápido** es el que domina la complejidad

