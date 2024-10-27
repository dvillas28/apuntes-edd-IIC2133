#clase12

Considerar [[Árboles M-arios]]

## Definición

Un **árbol B+ de orden $d$** es un árbol de búsqueda que almacena pares **(llave, valor)** y cumple con
1. Los nodos internos solo guardan llaves
2. La raíz tiene entre $1$ y $2d$ hijos
3. Los nodos internos tienen entre $d$ y $2d$ hijos
4. Las hojas están a la misma altura y guardan a lo más $2d$ pares (llave, valor) **ordenados por llave**
5. Las hojas están conectadas formando una lista doblemente ligada

- $d$: n° de hijos
- n° de llaves = $d-1$

Solo guardamos datos en las hojas

### Observaciones
- Siempre esta **balanceado**
- Mantiene la eficiencia de búsqueda:  $$\mathcal{O}(\log_{2d}(\#datos))$$
- Procedimientos eficientes de insertar/eliminar elementos
- Todos los nodos tienen un uso mínimo del 50% (menos el root)

## Estructura

![[Pasted image 20241018002128.png]]

Lista doblemente ligada: Sirve para realizar ***range queries***, necesitamos sucesores y antecesores

Son utilizados extensivamente para almacenar [[Indices]]


### Estructura del nodo

![[Pasted image 20241018002413.png]]

- El puntero $p_i$ apunta al directorio $k$ de llaves tal que $k_i \leq k \leq k_{i+1}$
- La llave y el puntero forman un *index entry*

El rango de llaves y punteros ($n$) viene dado por el **orden ($d$)** del B+ tree: $$ d \leq n \leq 2d \text{ para los intermedios}$$ $$ 1 \leq n \leq 2d \text{ para la raiz}$$
![[Pasted image 20241018185759.png]]


### Ejemplo de B+ *tree* con $d$ = 2

![[Pasted image 20241018002903.png]]
 
 Notar que las hojas contienen una estrella, esto indica que ahi esta almacenado el **dato** asociado a esa llave

## Búsqueda y *range queries* en B+ *trees*

Considerar la siguiente consulta que usa un índice sobre el atributo A

```sql
SELECT *
FROM R
WHERE A BETWEEN x AND y
```

1. Llamar P = `busquedaEnArbol(x, raiz)`
2. Realizar una búsqueda del mayor elemento $k*$ en P con $k*\leq x$
3. Hacer *scan* desde $k*$  sobre todos los valores menores o iguales a $y$
## Inserciones

Recordar: Un B+ *tree* siempre debe estar balanceado
Por ahora, **asumimos llave unica**

Para **insertar** un valor $k$
1. Llamar P = `busquedaEnArbol(k, raiz)`
2. Si la cantidad de llaves de P es menor a $2d$ (el nodo aun no se ha llenado) , insertar $k$ en P
3. En otro caso: debemos insertar $k$ en P y hacer *split* de \[P+K\], donde \[P+K\] = $k_1^*k_2^*\dots k_{2d}^*k_{2d+1}^*$

Para hacer **split** del nodo \[P+K\] de tamaño $2d + 1$
1. Asumir \[P+K\] = $k_1^*k_2^*\dots k_{2d}^*k_{2d+1}^*$ con $k_1 < k_{i+1}$
2. Dividir \[P+K\] en dos nodos
	- $P_1 = k_1^*\dots k_d^*$ y $P_2 = k_{d+1}^*\dots k_{2d+1}^*$ y reemplazar P por $P1$ y $P2$ en la lista doble ligada de los datos
3. Seleccionar el valor $k_{d+1}$ como **divisor** de $P_1$ y $P_2$
4. Reemplazar el puntero $p$ en el nodo $P'$ que apuntaba a el nodo $P$ por $p_1 k_{d+1} p_2$ donde $p_1$ apunta a $P_1$ y $p_1$ apunta a $P_2$
5. Iterar sobre el nodo de directorio $P'$ que apuntaba a $P$ (split de $P'$)

```c
Insert(k, root):
	P <- BusquedaEnArbol(k, root) // nodo donde se ubicará k
	Insert(k, P)
	if CantidadDeLlaves(P) > 2d:
		split(P) // reestablecer propiedades del B+
```

### Sobre el *split*

El *split* parte desde la hojas y continua hasta la raíz

IF (es necesario hacer split de todos los nodos y el nodo raíz esta lleno) entonces será necesario crear un nuevo nodo raíz - el unico momento en el que el B+ aumenta en altura

El nodo raíz es el **único que se le permite estar lleno al menos del 50%**

### Redistribución de vecinos

Una alternativa a *split*. Hace posible una inserción evitando el crecimiento del árbol

![[Pasted image 20241018191621.png]]

Se inserta en 6* en un nodo lleno y este queda con exceso
![[Pasted image 20241018191637.png]]

Movemos el mayor elemento del nodo con exceso al nodo vecino, **y usamos la llave de ese como nuevo separador, que reemplaza al que habia antes**
![[Pasted image 20241018191709.png]]

## Eliminaciones

Para **eliminar** un valor $k$
1. llamar P = `busquedaEnArbol(k, root)`
2. Si el espacio usado en P es mayor o igual a $d+1$, eliminar k en P
3. En otro caso, debemos eliminar $k$ en P y **re-balancear** \[P-K\]

### ejemplo1: nodo con espacio mayor a $d+1$

![[Pasted image 20241018192847.png]]![[Pasted image 20241018192853.png]]

### ejemplo2: caso contrario

![[Pasted image 20241018192941.png]]![[Pasted image 20241018192948.png]]
![[Pasted image 20241018193001.png]]

Ahora, si queremos eliminar el elemento 22*

![[Pasted image 20241018193108.png]]
![[Pasted image 20241018193117.png]]

Al mergear ambos nodos, ya no nos hace falta el separador 27

![[Pasted image 20241018193212.png]]

Pero ahora el directorio con queda invalido!

![[Pasted image 20241018193239.png]]

![[Pasted image 20241018193246.png]]

Obs: Si la raíz queda con un solo elemento, esta es la unica manera de decrementar la altura H del árbol

### Redistribución de vecinos en eliminación

En algunos casos es necesario **redistribuir** los elementos de un directorio en una eliminación, para no modificar la altura

#### ejemplo

![[Pasted image 20241018193448.png]]

![[Pasted image 20241018193506.png]]

## Eficiencia de los B+ *trees*

Considerar
- $n$: número de nodos
- $d$: cantidad (máxima) de datos en una hoja

El costo de cada operación (en I/O)
- Búsqueda: $\mathcal{O}(\log_{2d}(n))$
- Inserción: $\mathcal{O}(\log_{2d}(n))$
- Eliminación: $\mathcal{O}(\log_{2d}(n))$

## Duplicados en los B+ *trees*

Si ahora consideramos **duplicados**, tenemos varias opciones

- usar páginas con ***overflow***
- *data entries* extendidos con una llave compuesta (k, id) 
- permitir duplicados  y flexibilizar los intervalos del directorio $$k_i\leq k< k_{i+1} \rightarrow k_i\leq k \leq k_{i+1}$$
## Optimizaciones a B+ *trees*

- **Compresión** de *index keys* (o directorio): minimizar espacio ocupado
- *Bulk loading*