#clase11

## Convertir 2-3 en binario

Nos interesa convertir un [[Árboles 2-3]] en [[Arboles binarios de búsqueda]]. Nos centramos en los dos tipos de nodos del 2-3
- **2-nodo**: (1 llave y 0 hijos O 1 llave y 2 hijos).
	- Se puede representar como nodo de un ABB sin problemas
- **3-nodo**: (2 llaves y 0 hijos O 2 llaves y 3 hijos)
	- Se necesitan separar las llaves y los hijos

### Representación 2-nodo

![[Pasted image 20241014171153.png]]

### Representación 3-nodo

![[Pasted image 20241014171336.png]]

## Idea

Podemos darles color a los 3-nodos

![[Pasted image 20241014171430.png]]

## Definición

Un **árbol rojo-negro** es un ABB que cumple
1. Cada nodo es rojo o negro
2. La raíz del árbol es negra (si la raíz es roja, la pintamos de negro)
3. Si un nodo es rojo, sus hijos **deben** ser negros
4. La cantidad de nodos negros camino a cada hoja desde un nodo cualquiera debe ser la misma

Extra: las hojas vacías se consideran nodos negros
Extra2: los nodos rojos nos indican desbalance

## Balance y equivalencia con árbol 2-4

Al igual que en los árboles AVL, los cambios en el árbol pueden romper la propiedad de balance
- Tendremos una estrategia de restauración (rotaciones)
	- Pero, en lugar de usar `x.balance`, usaremos `x.color`

Para facilitar la comprensión del rebalanceo podemos notar que
- Los árboles 2-3 son fáciles de visualizar
- Pero no todo árbol rojo-negro tiene un árbol 2-3 equivalente
- Pero sí tiene un [[Árboles 2-4]] equivalente

Con este modelo, podemos tener árboles equivalentes, según

![[Pasted image 20241014172315.png]]

### ejemplo: obtener el árbol 2-4 equivalente al árbol rojo-negro

*Consultar con el apunte escrito*

## Inserciones en Árboles rojo-negro

Podemos usar el árbol 2-4 equivalente como ayuda
- Nos permitirá comprender mejor cómo efectuar **rotaciones** y **cambios de color**

Considerar el siguiente árbol

![[Pasted image 20241014175931.png]]

*consultar los apuntes escritos*
### Inserción Exterior

```c
// Inserción Exterior

input: Nodo x
output: null

FixBalance(x):
	if x fue inserción exterior:
		t <- x.uncle // tio de x
		if t.color == negro:
			g <- x.p.p // abuelo x
			Rotation(g, x.p)
			x.p.color <- negro
			g.color <- rojo
```

### Inserción Interior

```c
// Inserción Interior

input: Nodo x
output: null

FixBalance(x):
	if x fue inserción interior:
		t <- x.uncle // tio de x
		if t.color == negro:
			g <- x.p.p // abuelo de x
			Rotation(x.p, x)
			Rotation(g, x)
			x.color <- negro
			g.color <- rojo

```

### Inserción con tío rojo

```c
// Inserción con tío rojo
input: Nodo x
output: null

FixBalance(x):
	while x.p != null and x.p.color = rojo:
		t <- x.uncle // tio d ec
		if t.color == rojo:
			x.p.color <- negro
			t.color <- negro
			x.p.p.color <-rojo
			x <- x.p.p
	A.root.color <- negro
```

```

Al insertar, siempre lo hacemos como nodo rojo

Si el padre es negro, no hacemos nada

Si el padre es rojo, hay 2 casos
	1. Tío Negro: el nodo del árbol 2-4 crece, pero no colapsa
			rotaciones y cambios de color
	1. Tío Rojo: el nodo del árbol 2-4 colapsa y hay que subir
			cambios de color hacia la raíz
```

```c

FixBalance(x):
	while x.p != null and x.p.color == rojo:
		t <- x.uncle // tio de x
		if t.color == rojo:
			x.p.color <- negro
			t.color <- negro
			x.p.p.color <- rojo
			x <- x.p.p
		
		else:
			if x es hijo interior de x.p:
				Rotation(x.p, x)
				x <- x.p
			x.p.color <- negro
			x.p.p.color <- rojo
			Rotation(x.p.p, x)
	
	A.root.color <- negro
```

### ejemplo de creación de árbol rojo - negro

![[Pasted image 20241014184312.png]]

*consultar los apuntes escritos*