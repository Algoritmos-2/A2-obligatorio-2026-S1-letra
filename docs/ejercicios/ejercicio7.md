# Ejercicio 7 - Clasificación Iron Man

## Descripción

El **Iron Man** es una triatlón que combina tres disciplinas: natación, ciclismo y carrera a pie. Por motivos de organización los competidores no comienzan al mismo tiempo, por lo que el primero en cruzar la meta no es necesariamente el ganador: el resultado se determina sumando los tiempos parciales de cada competidor en las tres disciplinas.

Dada la lista de tiempos de los $L$ competidores, ordene a los competidores **de menor a mayor tiempo total** (menor tiempo equivale a mejor posición). El tiempo total del competidor $i$ se calcula como $T_i = N_i + B_i + C_i$.

## Entrada

- La primera línea contiene un entero $L$ ($1 \leq L \leq 10^6$), la cantidad de competidores.
- Las siguientes $L$ líneas contienen los tiempos de **natación** ($N_1, \dots, N_L$), una por competidor.
- Las siguientes $L$ líneas contienen los tiempos de **ciclismo** ($B_1, \dots, B_L$), una por competidor.
- Las siguientes $L$ líneas contienen los tiempos de **carrera a pie** ($C_1, \dots, C_L$), una por competidor.

Cada tiempo es un entero $1 \leq T \leq 10^6$. Los competidores se identifican por su orden de entrada, comenzando en $1$.

## Salida

Imprima $L$ líneas con los índices (1-indexados) de los competidores ordenados de menor a mayor tiempo total. Si dos competidores tienen el mismo tiempo total, deben aparecer en el mismo orden en que fueron ingresados.

## Restricciones

- Resolver utilizando **merge sort** (ordenamiento por divide and conquer).
- Complejidad temporal: $O(L \log L)$ en el peor caso.
- Complejidad espacial: $O(L)$ memoria auxiliar.

## Ejemplo

### Input

```
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
```

### Output

```
2
1
3
```

### Explicación

| Competidor | Natación | Ciclismo | Carrera | Total |
| ---------- | -------- | -------- | ------- | ----- |
| 1          | 10       | 20       | 30      | 60    |
| 2          | 12       | 18       | 28      | 58    |
| 3          | 9        | 25       | 35      | 69    |

Ordenando de menor a mayor tiempo total: **2** (58), **1** (60), **3** (69).
