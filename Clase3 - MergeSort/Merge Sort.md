#clase03 

Podemos utilizar el algoritmo [[Merge]] de una forma inteligente para ordenar una lista arbitraria

Esta forma inteligente es una estrategia llamada [[Dividir para conquistar]]

```c
input: Secuencia A
output: Secuencia ordenada B

MergeSort(A);
1 if |A| = 1 : return A
2 Dividir A en mitadaes A1 y A2
3 B1 <- MergeSort(A1)
4 B2 <- MergeSort(A2)
5 B <- Merge(B1, B2)
  return B
```

## Ejemplo de ejecución

![[Pasted image 20240819201816.png]]

## Correctitud
### Demostración de terminación
- Dividimos A hasta llegar a divisiones de 1 elementos
	- El algoritmo termina cuando se acaban las divisiones
		- Por lo tanto hay finitas recursiones
### Demostración de correctitud
- Demostramos que `MergeSort` termina, por lo que las líneas 3 y 4 pasan OK
- Ya demostramos que `Merge` es correcto
- Por lo tanto `MergeSort` es correcto

## Complejidad de tiempo y espacio

### Complejidad de tiempo
Necesitamos hacer un análisis de complejidad de tiempo

![[Pasted image 20240819205117.png]]

La complejidad de tiempo de `MergeSort` es $\mathcal{O}(n\log n)$
### Complejidad de espacio
- El caso base no ocupa memoria adicional
- Para $|A| = n$, la línea 5 (`Merge`) ocupa $\mathcal{O}(n)$ 
- Los llamados recursivos NO van acumulando memoria reservada
	- Por lo que no sumamos $\mathcal{O}(n)$ por llamado
	- La memoria adicional se puede reciclar
- La complejidad de memoria de `MergeSort` es $\mathcal{O}(n)$ (lo aporta el `Merge`)
## Síntesis *MergeSort*

![[Pasted image 20240819201930.png]]

![[Pasted image 20240819201942.png]]
