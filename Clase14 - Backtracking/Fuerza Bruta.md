#clase14 

Para resolver un CSP, podemos usar fuerza bruta

- Generar todas las asignaciones de variables
- Verificar si cada asignación para ver si cumple **todas** las restricciones
- Si se encuentra una asignación que cumple, se retorna como solución

Para un CSP $(X, D, C)$, esto requiere revisar en general las tuplas de $$D_1 \times D_2 \times \dots \times D_n $$