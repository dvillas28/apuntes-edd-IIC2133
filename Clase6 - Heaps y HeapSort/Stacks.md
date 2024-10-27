#clase06 

También llamadas Colas LIFO

Prioridad: Orden de llegada **invertido**
- 1° elemento es el menos prioritario: lleva más tiempo en el stack
- Ultimo elemento es el más prioritario: lleva menos tiempo en la cola

Tiene las siguientes operaciones
- **Inserción** (***push***): Se inserta en la cabeza de la cola
	- Arreglo: $\mathcal{O}(1)$ recorriendo al revés
	- Lista: $\mathcal{O}(1)$
- **Extracción** (***pop***): Se extrae (elimina) la cabeza de la cola
	- Arreglo: $\mathcal{O}(1)$ si no se reubica luego
	- Lista: $\mathcal{O}(1)$

