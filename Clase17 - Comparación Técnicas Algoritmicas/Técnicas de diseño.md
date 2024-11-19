#clase17

En este punto conocemos 4 estrategias 

- [[Dividir para conquistar]]
- [[Backtracking]]
- [[Algoritmos Codiciosos]]
- [[Programación dinámica]]

¿Cuándo preferimos una sobre otra en la práctica?

![[Pasted image 20241116223618.png]]

## Caso especial: Optimización

- Se pueden resolver con más de una 

Tenemos los siguientes criterios

- *Backtracking*:
	- Requiere computar **todas** las soluciones factibles
		- Útil en ciertas ocasiones
	- Muy costoso en tiempo
- Codicioso
	- Solo si es que existe estrategia optima probada
	- MUY eficientes en tiempo y memoria
- Dinámica
	- Solo si hay subestructura óptima
	- Puede ser eficiente en tiempo y memoria

## Sobre algoritmos codiciosos

Idea general para desmentir estrategias codiciosas falsas
- Debemos aprovechar la decisión de la estrategia
- Forzar a que cometa un error basado en su decisión local