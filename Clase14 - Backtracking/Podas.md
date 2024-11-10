#clase14 

*Backtracking* es capaz de determinar si una asignación puede terminar en solución

- Las soluciones inviables se **descartan** según las restricciones R del CSP
- Requiere llamadas recursivos. Posiblemente, **muchos** llamados

Podemos agregar nuevas restricciones que se deducen de las iniciales

Llamaremos **podas** a estas nuevas restricciones y se revisan junto a las originales

```c
isSolvable(X, D, R):
1 if X = null: return true
2 x <- alguna variable de X
3 for v in D_x:
4    if x = v no rompe R: // AQUI SE CHECKEAN LAS PODAS TAMBIEN
5        x <- v
6        if isSolvable(X - {x}, D, R):
7            return true
8        x <- null
9 return false
10
```

Pueden ser más costosas de checkear, peor vale la pena en la práctica
