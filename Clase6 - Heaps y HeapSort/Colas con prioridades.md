#clase06 

Hasta ahora, hemos usado arreglos y listas ligadas
- Representación directa de la memoria
- Permiten acceso por índice en tiempo $\mathcal{O}(1)$
- Usados en algoritmos de ordenación

Podemos aprovechar el acceso $\mathcal{O}(1)$ para definir una nueva EDD

## Definición

Una **cola de prioridades** es una EDD que permite
- Almacenar datos según cierta **prioridad**
- Consultar cuál es el dato **mas prioritario**
- Recorrer los datos en **orden de prioridad**

Ya conocemos dos tipos de prioridades
- Si interesa el que llegó ultimo (*LIFO*): [[Stacks]]
- Si interesa el que llegó primero (*FIFO*): [[Queues]]

Cola *highest priority first out* es una EDD que permite
- **Insertar** un dato con prioridad dada
- **Extraer** el dato con mayor prioridad
- Idealmente, **cambiar** la prioridad de un dato

A diferencia de las colas FIFO y LIFO, el orden de llegada no es equivalente a la posición de la cola

### Ejemplo

Definamos una cola A cuya prioridad sea el valor de los datos (todos son naturales)
Tenemos dos opciones extremas de almacenamiento de datos en la cola

1. Usar un arreglo sin orden entre elementos
2. Usar un arreglo que siempre este ordenado

La complejidad entre ambas opciones cambia
1. Arreglo sin orden
	- Inserción al final $\mathcal{O}(1)$
	- Extracción buscando máximo valor: $\mathcal{O}(n)$ (hay que buscarlo)
2. Arreglo ordenado por valor
	1. Inserción en posición correcta: $\mathcal{O}(n)$ (hay que buscarla)
	2. Extracción del ultimo elemento: $\mathcal{O}(1)$

Existe una mejor forma de hacer eficientes a las colas?

### Sobre el orden de los elementos

Para una EDD A, podemos distinguir dos tipos de orden
- Orden total, todos los elementos de A están ordenados
- Orden parcial: hay sub-sectores de A que están ordenados y conocemos bien la división de la sub-sectores

Para tener colas eficientes nos basta con tener un "cierto orden"
- Esto es lo que hacemos en [[Heaps]]