#clase08 
## Definición

Un **diccionario** es una EDD con las siguientes operaciones
- **Asociar** un valor a una llave
- **Actualizar** el valor asociado a una llave
- **Obtener** el valor asociado a una llave
- En ciertos casos, **eliminar** de la estructura una asociación llave-valor

Ejemplos
- RUT-nombre
- RUT-(nombre, apellido, edad, ...)

Objetivo central: facilitar la **búsqueda**
- Primero se busca la llave (si está o no está)
- Buscar = *buscar eficientemente*

¿Cómo almacenamos las llaves para lograr búsqueda eficiente?
- Hasta ahora tenemos arreglos y listas, pero tienen limitaciones ([[Limitaciones de arreglos y listas]])