#clase14 

*Backtracking* chequea los valores válidos en el dominio $D_i$ de la variable $x_i$ en un **orden arbitrario**

- No solo puede afectar el orden en que asignan valores
- También puede afectar el orden en que se itera sobre las variables disponibles

De hecho, si dispusiéramos de un **oráculo** que nos dice el mejor orden de asignación el problema se vuelve **lineal!**

Guiaremos la búsqueda según algunos criterios (falibles)

Llamaremos **heurísticas** a las estrategias para catalogar variables y valores según qué tan buenos son

```c
isSolvable(X, D, R):
1 if X = null: return true
2 x <- LA MEJOR VARIABLE DE X
3 for v in D_x de mejor a peor:
4    if x = v no rompe R:
5        x <- v
6        if isSolvable(X - {x}, D, R):
7            return true
8        x <- null
9 return false
10
```

Las heurísticas tratan de aproximar la realidad, pueden equivocarse

Posibles heurísticas

- Partir por la variable con el dominio más pequeño

![[Pasted image 20241109215149.png]]

- Partir por el valor con menos apariciones
![[Pasted image 20241109215201.png]]
## Ejemplo


![[Pasted image 20241109214514.png]]

Nos interesa minimizar la posibilidad de fracasar

![[Pasted image 20241109214536.png]]

Tenemos menos chances de fracasar si colocamos el 1 en la ultima columna

![[Pasted image 20241109214608.png]]