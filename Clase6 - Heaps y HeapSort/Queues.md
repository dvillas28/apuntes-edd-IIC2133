#clase06 

También llamadas Colas FIFO

Prioridad: Orden de llegada
- 1° elemento es el más prioritario: lleva más tiempo en la queue
- Ultimo elemento es el menos prioritario: lleva menos tiempo en la cola

Tiene las siguientes operaciones
- **Inserción** (***enqueue***): Se inserta al final de la cola
	- Arreglo: $\mathcal{O}(1)$ en general (salvo que se llene)
	- Lista: $\mathcal{O}(1)$ si se tiene un puntero a la cola
- **Extracción** (***dequeue***): Se extrae (elimina) la cabeza de la cola
	- Arreglo: $\mathcal{O}(1)$ si no se reubica luego
	- Lista: $\mathcal{O}(1)$


