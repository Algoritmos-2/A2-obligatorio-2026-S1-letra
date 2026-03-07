# Ejercicio 5 - Formación de equipos

## Descripción

En una universidad, se organizan actividades grupales donde los estudiantes deben dividirse en exactamente **dos equipos**. Sin embargo, existen **incompatibilidades** entre ciertos pares de estudiantes: dos estudiantes incompatibles no pueden pertenecer al mismo equipo.

Dado el conjunto de estudiantes y sus incompatibilidades, determine si es posible dividir a todos los estudiantes en exactamente dos equipos de manera que no haya dos estudiantes incompatibles en el mismo equipo.

Los estudiantes se identifican con números del $1$ al $V$. El grafo puede no ser conexo (puede haber estudiantes sin incompatibilidades o grupos aislados).

## Entrada

- La primera línea contiene dos enteros $V$ y $A$ ($1 \leq V \leq 10^5$, $0 \leq A \leq 10^5$), donde $V$ es la cantidad de vértices (estudiantes) y $A$ es la cantidad de aristas (incompatibilidades).
- Las siguientes $A$ líneas contienen dos enteros $u$ y $v$ ($1 \leq u, v \leq V$, $u \neq v$), indicando que los estudiantes $u$ y $v$ son incompatibles.

## Salida

Imprima `SI` si es posible dividir a los estudiantes en dos equipos sin que haya incompatibles en el mismo equipo. En caso contrario, imprima `NO`.

## Restricciones

- Utilizar un **grafo** para modelar las incompatibilidades.
- Resolver en orden temporal: $O(V + A)$ en el peor caso.

## Ejemplo

### Input 1

```
4 4
1 2
2 3
3 4
4 1
```

### Output 1

```
SI
```

### Explicación 1

Estudiantes: 1, 2, 3, 4.

Incompatibilidades:

| Par   | Incompatibles |
| ----- | ------------- |
| 1 - 2 | si            |
| 2 - 3 | si            |
| 3 - 4 | si            |
| 4 - 1 | si            |

```cytoscape
{"nodes": [1, 2, 3, 4], "edges": [[1,2],[2,3],[3,4],[4,1]]}
```

Se puede dividir en:
- Equipo A: {1, 3}
- Equipo B: {2, 4}

Ningún par de incompatibles queda en el mismo equipo. Resultado: **SI**.

---

### Input 2

```
3 3
1 2
2 3
3 1
```

### Output 2

```
NO
```

### Explicación 2

Estudiantes: 1, 2, 3.

```cytoscape
{"nodes": [1, 2, 3], "edges": [[1,2],[2,3],[3,1]]}
```

Forman un ciclo de longitud impar (triángulo). No importa cómo se dividan, siempre habrá al menos un par de incompatibles en el mismo equipo:

| Intento               | Conflicto           |
| --------------------- | ------------------- |
| A={1,2}, B={3}        | 1-2 en mismo equipo |
| A={1,3}, B={2}        | 1-3 en mismo equipo |
| A={2,3}, B={1}        | 2-3 en mismo equipo |
| A={1}, B={2,3}        | 2-3 en mismo equipo |

Resultado: **NO**.

---

### Input 3

```
6 4
1 2
3 4
5 6
2 3
```

### Output 3

```
SI
```

### Explicación 3

Estudiantes: 1, 2, 3, 4, 5, 6.

```cytoscape
{"nodes": [1, 2, 3, 4, 5, 6], "edges": [[1,2],[2,3],[3,4],[5,6]]}
```

Hay dos componentes conexas: {1,2,3,4} y {5,6}. Ambas son bipartitas:

| Componente | Equipo A | Equipo B |
| ---------- | -------- | -------- |
| {1,2,3,4}  | {1, 3}   | {2, 4}   |
| {5,6}      | {5}      | {6}      |

Resultado: **SI**.

---

### Input 4

```
7 8
1 2
2 3
3 4
4 5
5 3
1 6
6 7
7 1
```

### Output 4

```
NO
```

### Explicación 4

Estudiantes: 1, 2, 3, 4, 5, 6, 7.

```cytoscape
{"nodes": [1, 2, 3, 4, 5, 6, 7], "edges": [[1,2],[2,3],[3,4],[4,5],[5,3],[1,6],[6,7],[7,1]]}
```

El subgrafo formado por los vértices 3, 4 y 5 forma un ciclo de longitud impar (triángulo). No es posible dividir estos tres vértices en dos equipos sin que haya incompatibles juntos.

Resultado: **NO**.
