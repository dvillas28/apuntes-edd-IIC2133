#clase23 

![[Pasted image 20241207193244.png]]

Considerando el siguiente grafo dirigido con **costos negativos**, comprobar que Dijkstra no entrega la ruta con el menor costo desde A hasta B. 

![[Pasted image 20241207193329.png]]

Llevaremos en una tabla el estado de $d[X], \pi[X]$, y $Q$ al inicio de la iteración T del loop, recordar que $$d[X]:= \text{ menor costo acumulado hasta } X$$ $$\pi[X]:= \text{ ancestro de } X \text{ en ese camino}$$

Al inicio de la primera iteración, tenemos los valores iniciales y el nodo de partida como **más prioritario** en $Q$ (que además es gris)

![[Pasted image 20241207193857.png]]


Al revisar los vecinos de A, actualizamos los costos y los ancestros, pues tenemos un camino de largo 1, que es mejor que el costo $\infty$ 

Además, al descubrir B y C, se pintan grises y se agregan a la cola **respetando prioridad** dada por $d[X]$

Entonces, revisamos todas las conexiones desde A, y lo terminamos

![[Pasted image 20241207194047.png]]

Seguimos y por prioridad $Q$ entrega a B como siguiente elemento a revisar. Dado que no tiene vecinos, lo terminamos

![[Pasted image 20241207194134.png]]

Ahora extraemos de $Q$ a C, y como su único vecino ya está terminado, terminamos a C también

![[Pasted image 20241207194204.png]]

Luego tenemos el estado final de los parámetros, lo que nos entrega la ruta encontrada por Dijkstra

![[Pasted image 20241207194245.png]]

Dijkstra se basa en un recorrido BFS del grafo

- **Asume** si ya llegamos en $k$ pasos a un nodo $u$ con costo $d[u]$, no podemos llegar con un costo menos en $k+1$ pasos
- Esto simplifica el análisis y permite no revisar aristas cuando ya hemos terminado un nodo
- Recordar: si el nodo está terminado (color negro), **ya no cambia su** $d[u]$

Esto funciona cuando los costos son no negativos, pues una arista $k+1$ mantiene o incrementa el costo ya alcanzado en $k$ pasos

![[Pasted image 20241207200028.png]]

![[Pasted image 20241207200152.png]]

Solucion: [[Bellman-Ford]]

