## Definición

Dada una secuencia `A[0...n-1]`, sea `B[0...n-1]` la secuencia resultante de ordenar `A` usando un algoritmo de ordenación $\mathcal{S}$. Sean `a, a'` elementos en `A` tales que para el algoritmo $\mathcal{A}$ son equivalentes y `a` aparece antes que `a'` en `A`. Diremos que $\mathcal{S}$ es **estable** si los elementos correspondientes `b, b'` aparecen en el **mismo orden relativo** en `B`

**Idea principal**: Si ordenamos por el segundo dígito, un orden estable dejaría elementos que comparten segundo dígito en el mismo orden en que nos llegaron