#clase04

Un algoritmo para basado en la estrategia dividir para conquistar

```c
// Buscamos al elemento x en A, entre las posiciones [i, f]

BinarySearch(A, x, i, f):
1 if f < i: return -1
2 m <- floor((i+2)/2) // parte entera
3 if A[m] = x : return m
4 if A[m] > x : 
5     return BinarySearch(A, x, i, m-1)
6 return BinarySearch(A, x, m+1, f)

// Si |A| = n, y queremos buscar por todo el arreglo llamamos
// BinarySearch(A, x, 0, n-1)
```

- Se escoge un pivote central (línea 2)
- La naturaleza de la búsqueda hace que sea necesario resolver **solo uno de los sub-problemas**
- La solución del problema es exactamente la solución al llamado recursivo

