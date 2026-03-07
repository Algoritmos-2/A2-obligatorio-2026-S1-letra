# Ejercicio 2 - Competencia académica

## Descripción

En una competencia académica interuniversitaria, los participantes acumulan puntos a lo largo de varias rondas. Al finalizar la competencia, se debe determinar el ganador según las siguientes reglas:

- Si al final de la competencia solo hay un participante con el puntaje máximo, ese es el ganador.
- Si dos o más participantes terminan con el mismo puntaje máximo, gana aquel que **alcanzó dicho puntaje primero** durante el transcurso de la competencia.

En cada ronda, un participante gana o pierde una cantidad determinada de puntos. Los resultados se registran en el formato `[nombre] [puntaje]`, donde `[nombre]` es el nombre del participante y `[puntaje]` es la cantidad de puntos obtenidos en esa ronda (un número entero que puede ser negativo si el participante perdió puntos).

Inicialmente, cada participante tiene **0 puntos**. Se garantiza que al final de la competencia al menos un participante tiene un puntaje positivo.

Dado el registro de la competencia, determine el nombre del ganador.

## Entrada

- La primera línea contiene un entero $n$ ($1 \leq n \leq 10^6$), la cantidad de rondas jugadas.
- Las siguientes $n$ líneas contienen la información de cada ronda en formato `nombre puntaje`, en orden cronológico, donde `nombre` es una cadena de letras latinas minúsculas con longitud entre 1 y 32, y `puntaje` es un entero entre $-1000$ y $1000$ inclusive.

## Salida

Imprima el nombre del ganador.

## Restricciones

- Utilizar una **tabla de hash cerrada** (direccionamiento abierto) con **doble hashing** para resolver el problema.
- Resolver en orden temporal: $O(N)$ promedio, siendo $N$ la cantidad de rondas.

## Ejemplo

### Input 1

```
3
mike 3
andrew 5
mike 2
```

### Output 1

```
andrew
```

### Explicación 1

Puntajes finales: mike = $3 + 2 = 5$, andrew = $5$.

Ambos terminan con $5$ puntos (el máximo). ¿Quién alcanzó $5$ primero?

| Ronda | Jugador  | Cambio | Puntaje acumulado |
| ----- | -------- | ------ | ----------------- |
| 1     | mike     | +3     | mike: 3           |
| 2     | andrew   | +5     | andrew: **5**     |
| 3     | mike     | +2     | mike: **5**       |

Andrew alcanzó $5$ en la ronda 2, mike en la ronda 3. Ganador: **andrew**.

---

### Input 2

```
3
andrew 3
andrew 2
mike 5
```

### Output 2

```
andrew
```

### Explicación 2

Puntajes finales: andrew = $3 + 2 = 5$, mike = $5$.

Ambos terminan con $5$ puntos.

| Ronda | Jugador  | Cambio | Puntaje acumulado |
| ----- | -------- | ------ | ----------------- |
| 1     | andrew   | +3     | andrew: 3         |
| 2     | andrew   | +2     | andrew: **5**     |
| 3     | mike     | +5     | mike: **5**       |

Andrew alcanzó $5$ en la ronda 2, mike en la ronda 3. Ganador: **andrew**.

---

### Input 3

```
5
alice 50
bob 30
charlie 70
alice -10
bob 40
```

### Output 3

```
charlie
```

### Explicación 3

Puntajes finales: alice = $50 - 10 = 40$, bob = $30 + 40 = 70$, charlie = $70$.

El puntaje máximo es $70$. Tanto bob como charlie terminan con $70$.

| Ronda | Jugador  | Cambio | Puntaje acumulado              |
| ----- | -------- | ------ | ------------------------------ |
| 1     | alice    | +50    | alice: 50                      |
| 2     | bob      | +30    | bob: 30                        |
| 3     | charlie  | +70    | charlie: **70**                |
| 4     | alice    | -10    | alice: 40                      |
| 5     | bob      | +40    | bob: **70**                    |

Charlie alcanzó $70$ en la ronda 3, bob en la ronda 5. Ganador: **charlie**.

---

### Input 4

```
6
ana 100
luis 80
ana -60
luis 20
pedro 100
ana 60
```

### Output 4

```
ana
```

### Explicación 4

Puntajes finales: ana = $100 - 60 + 60 = 100$, luis = $80 + 20 = 100$, pedro = $100$.

Los tres terminan con $100$ puntos. Este ejemplo muestra que un participante puede **perder puntos y luego recuperarse**, pero lo que importa es quién alcanzó el puntaje máximo final primero durante la competencia.

| Ronda | Jugador | Cambio | Puntaje acumulado                |
| ----- | ------- | ------ | -------------------------------- |
| 1     | ana     | +100   | ana: **100**                     |
| 2     | luis    | +80    | luis: 80                         |
| 3     | ana     | -60    | ana: 40                          |
| 4     | luis    | +20    | luis: **100**                    |
| 5     | pedro   | +100   | pedro: **100**                   |
| 6     | ana     | +60    | ana: **100** (segunda vez)       |

Ana alcanzó $100$ en la ronda 1 (antes que nadie, aunque luego bajó y volvió a subir). Luis en la ronda 4 y pedro en la ronda 5. Ganador: **ana**.

---

### Input 5

```
4
ana 100
ana -50
ana -40
bob 90
```

### Output 5

```
bob
```

### Explicación 5

Puntajes finales: ana = $100 - 50 - 40 = 10$, bob = $90$.

El puntaje máximo final es $90$ (bob). Aunque ana alcanzó $100$ durante la ronda 1, su puntaje final es $10$. Solo importa el puntaje **al final** de la competencia para determinar el máximo; el desempate cronológico aplica únicamente entre quienes **terminaron** con ese puntaje máximo.

| Ronda | Jugador | Cambio | Puntaje acumulado |
| ----- | ------- | ------ | ----------------- |
| 1     | ana     | +100   | ana: 100          |
| 2     | ana     | -50    | ana: 50           |
| 3     | ana     | -40    | ana: 10           |
| 4     | bob     | +90    | bob: **90**       |

Bob es el único con el puntaje máximo final. Ganador: **bob**.