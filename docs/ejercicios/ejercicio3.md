# Ejercicio 3 - Urgencias

## Descripción

Una clínica recibe un flujo constante de pacientes. Cada paciente llega en un momento diferente y con un nivel de urgencia distinto. Se necesita implementar un sistema que determine el orden en que los pacientes serán atendidos, priorizando según las siguientes reglas:

1. Se atiende primero al paciente con **mayor nivel de urgencia** (mayor número).
2. En caso de empate en urgencia, se atiende primero al paciente que **llegó antes** (menor hora de llegada).
3. En caso de empate en urgencia y hora de llegada, se atiende primero al paciente que **fue ingresado primero** en el sistema (orden de aparición en la entrada).

Cada paciente se identifica por un número $P$, llega a la hora $T$ (en formato 24 horas, de `0000` a `2359`) y tiene un nivel de urgencia $U$.

## Entrada

- La primera línea contiene un entero $N$ ($1 \leq N \leq 10^6$), la cantidad de pacientes.
- Las siguientes $N$ líneas contienen un entero $P$, una cadena $T$ y un entero $U$ separados por espacio:
  - $P$: identificador del paciente.
  - $T$: hora de llegada en formato de 4 dígitos (`0000` a `2359`).
  - $U$: nivel de urgencia.

## Salida

Imprima $N$ líneas, cada una con el identificador del paciente en el orden en que serán atendidos.

## Restricciones

- Utilizar un **heap binario** para resolver el problema.
- Resolver en orden temporal: $O(N \log N)$ en el peor caso, siendo $N$ la cantidad de pacientes.

## Ejemplo

### Input 1

```
4
10 0800 3
15 1300 2
7 0930 3
9 1800 1
```

### Output 1

```
10
7
15
9
```

### Explicación 1

| Paciente | Hora de llegada | Urgencia | Orden de ingreso |
| -------- | --------------- | -------- | ---------------- |
| 10       | 08:00           | 3        | 1                |
| 15       | 13:00           | 2        | 2                |
| 7        | 09:30           | 3        | 3                |
| 9        | 18:00           | 1        | 4                |

- Pacientes 10 y 7 tienen la mayor urgencia (3). Desempate por hora: paciente 10 llegó a las 08:00 y paciente 7 a las 09:30. Se atiende primero al **10**, luego al **7**.
- Siguiente urgencia (2): paciente **15**.
- Menor urgencia (1): paciente **9**.

---

### Input 2

```
3
1 1400 5
2 1400 5
3 1400 5
```

### Output 2

```
1
2
3
```

### Explicación 2

Los tres pacientes tienen la misma urgencia ($5$) y la misma hora de llegada (`1400`). Se aplica la tercera regla de desempate: se atienden en el **orden en que fueron ingresados** al sistema.

---

### Input 3

```
5
100 2200 1
200 0730 4
300 0730 4
400 0615 4
500 2200 1
```

### Output 3

```
400
200
300
100
500
```

### Explicación 3

| Paciente | Hora de llegada | Urgencia | Orden de ingreso |
| -------- | --------------- | -------- | ---------------- |
| 100      | 22:00           | 1        | 1                |
| 200      | 07:30           | 4        | 2                |
| 300      | 07:30           | 4        | 3                |
| 400      | 06:15           | 4        | 4                |
| 500      | 22:00           | 1        | 5                |

- Urgencia 4: pacientes 200, 300, 400. Desempate por hora: paciente 400 (`0615`) va primero. Pacientes 200 y 300 llegaron a la misma hora (`0730`), desempate por orden de ingreso: **200** antes que **300**.
- Urgencia 1: pacientes 100 y 500. Misma hora (`2200`), desempate por orden de ingreso: **100** antes que **500**.

Resultado: 400, 200, 300, 100, 500.

---

### Input 4

```
7
1 0600 5
2 0715 3
3 0900 5
4 0600 3
5 1030 1
6 0715 5
7 0900 3
```

### Output 4

```
1
6
3
4
2
7
5
```

### Explicación 4

Este ejemplo combina todas las reglas de desempate:

| Paciente | Hora de llegada | Urgencia | Orden de ingreso |
| -------- | --------------- | -------- | ---------------- |
| 1        | 06:00           | 5        | 1                |
| 2        | 07:15           | 3        | 2                |
| 3        | 09:00           | 5        | 3                |
| 4        | 06:00           | 3        | 4                |
| 5        | 10:30           | 1        | 5                |
| 6        | 07:15           | 5        | 6                |
| 7        | 09:00           | 3        | 7                |

- **Urgencia 5** (pacientes 1, 3, 6): por hora → 1 (`0600`), luego 6 (`0715`), luego 3 (`0900`).
- **Urgencia 3** (pacientes 2, 4, 7): por hora → 4 (`0600`), luego 2 (`0715`), luego 7 (`0900`).
- **Urgencia 1** (paciente 5): solo uno, va último.

Resultado: 1, 6, 3, 4, 2, 7, 5.