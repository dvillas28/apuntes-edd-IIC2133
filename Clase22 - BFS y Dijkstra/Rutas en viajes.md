#clase22

## Motivación

Considerar el problema de planificar un viaje en auto entre dos ciudades
- Podemos pensar en un grafo **dirigido**: caminos y puntos de intersección
- El auto tiene un consumo
- El combustible tiene un costo
- Cada camino tiene un largo conocido
- Cada camino, puede tener un peaje

El costo $\sigma_i$ de usar el camino $i$ engloba estos costos

Esto se puede representar con un **[[Grafo]] dirigido con costos**

![[Pasted image 20241207140020.png]]

Observación: en este problema, los costos son **no negativos**

Nuestro objetivo es obtener la ruta más barata (suma de los costos debe ser mínima). Para resolver este problema utilizamos [[Dijkstra]]

Si consideramos el caso especial $\sigma_i = K$ , el problema trata de buscar **la ruta mas corta** (con la menor cantidad de aristas involucradas). 

Para resolver este problema simplificado podemos usar [[BFS]]


![[Pasted image 20241207140126.png]]