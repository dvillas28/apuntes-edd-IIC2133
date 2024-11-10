#clase14 

*Backtracking* chequea todos los valores posibles en el dominio $D_i$ de la variable $x_i$

- Existen restricciones que invalidan ciertos valores de $D_i$
- *Backtracking* clásico los revisa igual
- Esas soluciones parciales nunca serán válidas

¿Podemos hacerlo mejor?: Cambiaremos los dominios de las demás variables luego de una asignación

Llamaremos **propagación** a la acción de modificar dominios luego de una asignación

```c
isSolvable(X, D, R):
1 if X = null: return true
2 x <- alguna variable de X
3 for v in D_x:
4    if x = v no rompe R:
5        x <- v, propagar // asignacion, modificar los dominios
6        if isSolvable(X - {x}, D, R):
7            return true
8        x <- null, propagar // asignacion, modificar los dominios
9 return false
10                                  
```

Hay que tener ojo al deshacer asignaciones, pues hay que reestablecer dominios propagados

## Ejemplo

![[Pasted image 20241109213238.png]]

![[Pasted image 20241109213244.png]]