# Ejercicio 7 - Clasificación Iron Man

## Descripción

En Uruguay, como todos los años, se lleva a cabo el famoso **Iron Man**, una triatlón que, como su nombre lo indica, consta de tres disciplinas:

- Natación  
- Ciclismo  
- Carrera a pie  

Por motivos de organización, los competidores **no comienzan la carrera al mismo tiempo**. Debido a esto, el primero en cruzar la meta no necesariamente es el ganador.

El resultado final se determina sumando los tiempos de cada competidor en las tres disciplinas.

Su tarea es **ordenar a los competidores según su tiempo total**, de menor a mayor (menor tiempo = mejor posición).

## Entrada

- La primera línea contiene un entero positivo $L$, la cantidad de competidores.
- Las siguientes $L$ líneas contienen los tiempos de natación:  
  $N_1, N_2, \dots, N_L$
- Las siguientes $L$ líneas contienen los tiempos de ciclismo:  
  $B_1, B_2, \dots, B_L$
- Las siguientes $L$ líneas contienen los tiempos de carrera a pie:  
  $C_1, C_2, \dots, C_L$

## Salida

Imprimir $L$ líneas con el orden de los competidores:

- $O_1, O_2, \dots, O_L$

Donde $O_i$ representa el índice del competidor en la posición $i$ (ordenados de menor a mayor tiempo total).

## Notas

- El tiempo total de cada competidor se calcula como:  
  $T_i = N_i + B_i + C_i$
- En caso de empate, se puede mantener el orden original de los competidores.

## Restricciones

- La solución debe implementarse utilizando la técnica de **Divide and Conquer (D&C)**.
- Complejidad esperada: $O(L \log L)$.

## Ejemplo

### Input
3
10
12
9
20
18
25
30
28
35

### Cálculo de tiempos

| Corredor | Natación | Ciclismo | Carrera | Total |
|----------|----------|----------|---------|--------|
| 1        | 10       | 20       | 30      | 60     |
| 2        | 12       | 18       | 28      | 58     |
| 3        | 9        | 25       | 35      | 69     |

### Orden

Ordenando por tiempo total (menor a mayor):

1. Corredor 2 → 58  
2. Corredor 1 → 60  
3. Corredor 3 → 69  

### Output
2
1
3