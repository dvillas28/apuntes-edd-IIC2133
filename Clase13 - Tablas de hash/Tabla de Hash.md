#clase13

## Introducción

### [[Diccionario]]s

Los [[Arboles binarios de búsqueda]] efectivamente soportan las operaciones de un diccionario
- La complejidad de las operaciones es $\mathcal{O}(h)$ 
- Cuando están balanceados, $h \in \mathcal{O}(\log (n))$ para $n$ llaves almacenadas

Los ABB no solo soportan las operaciones de diccionario
- La propiedad de ABB garantiza que los datos están **ordenados**
- Si el orden es importante, eso es necesario

El principal objetivo de los diccionarios es **búsqueda eficiente** de llaves
- el objetivo secundario es **inserción/modificación eficiente** de pares llave-valor
- Con esto, el orden de las llaves deja de ser relevante

Podemos buscar e insertar más rápido si nos olvidamos de mantener el orden

### Escenario ideal

Considerar el siguiente escenario ideal
- Conjunto de llaves posibles $K = \{0,\dots,11\}$ fijo y conocido
- Dada una llave $k \in K$, interesa saber si esta se encuentra asociada a un valor es la EDD

Podemos manejar este escenario se puede manejar con la siguiente EDD básica
- Arreglo $A[0,\dots,11]$ iniciado con $\emptyset$ en cada celda
- No almacenamos las llaves en las celdas, sino un puntero al valor asociado a la llave $k$ en $A[k]$ 
	- i.e. $A[k] \leftrightarrow$ no hay valor asociado a $k$ en $A$ 

![[Pasted image 20241026193839.png]]

En la estructura $A$ los accesos a $A[k]$ son **accesos por índice**
- Verificar si $A[k] = \emptyset$ es $\mathcal{O}(1)$
- Insertar y modificar el valor en $A[k]$ es $\mathcal{O}(1)$

No solo las operaciones deseadas son súper eficientes
- A diferencia de un ABB, se almacena solo un puntero al valor guardado
- No se usan punteros a padres-hijos para mantener la estructura

### ¿Qué tan ideal es este escenario?

El escenario de llaves $K$ puede ocurrir en aplicaciones prácticas
- Con un rango de valores razonables
- Llaves siempre naturales (para ser usadas como índices de arreglos)

![[Pasted image 20241026194402.png]]

![[Pasted image 20241026194817.png]]

## Funciones de hash

Dado un espacio de llaves $K$ y un natural $m > 0$, una **función de hash** se define como $$h: K \rightarrow \{0,\dots,m-1\}$$
Dado $k \in K$ llamaremos **valor de hash de $k$** a la evaluación $h(k)$

Notar que
- Una función de hash nos permite mapear un espacio de llaves a otro más pequeño (con $m$ razonable)
- Una función de hash no necesariamente es **inyectiva**
- Si $m < |K|$, no puede ser inyectiva
- En la practica, $m$ << $|K|$

## Tablas de hash

Dado $m >0$ y un conjunto de llaves $K$, una **tabla de hash** $A$ es una EDD que asocia valores a llaves indexadas usando una función de hash $h: K \rightarrow \{0,\dots,m-1\}$. Diremos que tal $A$ es de tamaño $m$

![[Pasted image 20241026195441.png]]

El ejemplo ideal que vimos antes es una tabla de hash

## Operaciones en la tabla de Hash

Para *hashing* general, las operaciones serían

```
HashSearch(A,k):
	return A[h(k)]

HashInsert(A,k,v):
	A[h(k)] = v

HashDelete(A,k):
	A[h(k)] = null

```

Pero sabemos que $h$ no es necesariamente inyectiva.
	Puede ocurrir una **colisión** $h(k_1) = h(k_2)$ para $k_1 \neq k_2$ 

### Manejo de colisiones

### Hashing modular

Considerar la siguiente función de hash: $$h(k) = k \text{ mod } m$$
- $h(k) \in \{0,\dots,m-1\},  \forall k$ 
- Todas las llaves con el mismo resto al dividir entre $m$ generan una colision

![[Pasted image 20241027190903.png]]

### Inserción

#### Inserción con encadenamiento

- Cada valor guardado en un nodo de una lista ligada
- Cada colisión agrega un nodo al principio/final de la lista

![[Pasted image 20241027191012.png]]

Las operaciones de diccionario son las siguientes
```
ChainedHashSearch(A,k):
	Buscar llave en A[h(k)]

ChainedHashInsert(A,k,v):
	Insertar (k,v) como cabeza de A[h(k)]

ChainedHashDelete(A,k):
	Eliminar llave k de A[h(k)]
```

- La complejidad de estas operaciones depende de qué tan largas sean las listas
- Una buena función de hash repartiría las llaves de manera más o menos homogénea

![[Pasted image 20241027191242.png]]

#### Inserción con sondeo lineal

**Direccionamiento abierto**
- Buscar sistemáticamente una celda vacía
- Puede producir nuevas colisiones no previstas por $h$

El **sondeo lineal** inserta en la primera celda vacía a la derecha de la colisión

![[Pasted image 20241027191426.png]]


### Búsqueda con sondeo lineal

Si las inserciones son con sondeo lineal, la búsqueda debe tenerlo en cuenta
- No necesariamente $k$ está guardado en $A[h(k)]$
- Debemos revisar esa celda, y si no corresponde, buscar **hacia adelante**

![[Pasted image 20241027191715.png]]

¿Cómo detectamos si la llave no está?
- Comenzamos la búsqueda en $A[h(k)]$
- Si al buscar a la derecha llegamos a un $\emptyset$ significa que no está

![[Pasted image 20241027191819.png]]

### Eliminación con sondeo lineal

Tenemos un problema
- Si borramos una llave la reemplazamos por $\emptyset$

![[Pasted image 20241027191857.png]]

No se recomienda usar sondeo lineal si tenemos que eliminar
**Si necesitamos eliminación**, es mejor usar encadenamiento

### Otros tipos de sondeo

- Sondeo lineal
	- Si $h(k) = H$, para alguna constante $d$ buscamos en $$H, H+d, H+2d,\dots$$
	- Se debe cumplir $d=1$ o que $d$ o $m$ son primos relativos

- Sondeo cuadrático
	- Si $h(k) = H$ buscamos en $$H,H+1,H+4,H+9,\dots$$
- Doble hashing
	- Usamos dos funciones de hash $h_1, h_2$ y buscamos en $$h_1(k), h_1(k)+h_2(k), h_1(k) + 2h_2(k), \dots$$

Todos ellos presentan el problema de la eliminación

## Factor de carga

Dado que las colisiones impactan la tabla, nos interesa medir cuántos datos tenemos almacenados

Para esto tenemos el [[Factor de carga]]

Según la estrategia de resolución de colisiones
- Encadenamiento: es aceptable si $\lambda \approx 1$
- Direccionamiento abierto: $\lambda > 0.5$ resulta en inserciones y búsquedas muy lentas

## *Rehashing*

Si $\lambda$ es grande y ya no es aceptable, las operaciones se vuelven costosas

Una solución es hacer *rehashing*
- Se crea una nueva tabla más grande, aproximadamente del doble del tamaño original
- Como es espacio de índices ya no es de tamaño $m$, se define una nueva función de hash
- Se mueven los datos a la nueva tabla

Esta es una operación costosa para las tablas de hash
- Es $\mathcal{O}(n)$ para $n$ datos insertados
- No obstante, es **infrecuente**
## Síntesis

![[Pasted image 20241027192900.png]]


