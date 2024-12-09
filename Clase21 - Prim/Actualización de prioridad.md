#clase21 

Ya vimos que las colas de prioridad implementadas como [[Heaps]] permiten
- Insertar valores con prioridad
- Extraer el más prioritario

En algunos contextos además necesitamos **actualizar** prioridad cuando cambie el costo óptimo

1. Cambiamos la prioridad del nodo del *heap*
2. Hacemos intercambios hacia arriba si es necesario

La propiedad del *heap* permite que esta operación solo afecte nodos en la ruta del nodo a la raíz

```c
input: heap representado como arreglo H[0...n-1]
	   indice i,
	   nueva prioridad k > H[i]

IncreaseKey(H, i, k):
1 H[i] <- k
2 while (i > 0) and (H[Parent(i)] < H[i]):
3     swap(H[i], H[Parent(i)])
4     i <- Parent(i)
```

En tiempo $\mathcal{O}(\log V)$ actualizamos la prioridad y mantenemos el *heap*