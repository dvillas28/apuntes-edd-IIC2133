#clase00

Para describir algoritmos
## Notación
- Control de flujo: `if, else, while, for`
- Lenguaje matemático: operaciones lógicas, de conjuntos, vectoriales
- Atributos, métodos y subíndices
- Podemos usar lenguaje natural cuando es más claro que lo anterior

### Ejemplo
````
// algoritmo simple para identificar si un número es primo

input: Número natural n >= 2
output: Valor booleano

isprime(n):
	for i in [2...sqrt(n)]:
		if n mod i = 0: // if n es divisible por i (lenguaje natural)
			return false
	return true
```