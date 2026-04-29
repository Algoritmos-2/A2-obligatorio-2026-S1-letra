# Ejercicio 10 - Countdown

## Descripción

Maurice Moss, fanático declarado del programa de televisión británico **Countdown**, ha decidido finalmente postularse como participante. Para prepararse, practica obsesivamente el famoso _numbers round_: dado un conjunto de cartas con números y un número objetivo, debe combinarlos usando las operaciones aritméticas básicas (`+`, `-`, `*`, `/`) para alcanzar exactamente dicho objetivo.

A diferencia del juego original, donde el participante puede elegir cuántas cartas usar, Moss quiere entrenarse con la regla más exigente posible: **todas las cartas deben ser utilizadas exactamente una vez**.

Cada operación toma dos números del conjunto y los reemplaza por el resultado de aplicarles la operación, dejando un número menos en el conjunto. El proceso se repite hasta que queda un único valor. Si ese valor coincide con el objetivo, la combinación es válida.

Dado un conjunto de cartas y un número objetivo, determine si es posible combinarlas para alcanzar exactamente el objetivo.

## Entrada

- La primera línea contiene un entero positivo $n$ ($1 \leq n \leq 10$), la cantidad de cartas.
- Las siguientes $n$ líneas contienen un entero cada una, el valor de cada carta.
- La última línea contiene un entero, el valor objetivo.

## Salida

Imprima `1` si es posible alcanzar el objetivo utilizando todas las cartas exactamente una vez. Imprima `0` en caso contrario.

## Restricciones

- Utilizar **backtracking** para explorar las combinaciones posibles.
- Como la operación de división puede generar resultados no enteros, todos los cálculos intermedios deben realizarse con números de **punto flotante** (`double`). Para comparar valores se debe utilizar una tolerancia $\varepsilon = 10^{-6}$, ya que las operaciones de punto flotante pueden acumular errores de redondeo.

Ejemplo en C++:

```cpp
const double EPS = 1e-6;

if (abs(a - b) < EPS) {
    // a y b se consideran iguales
}
```

Ejemplo en Java:

```java
static final double EPS = 1e-6;

if (abs(a - b) < EPS) {
    // a y b se consideran iguales
}
```

## Ejemplo

### Input 1

```
4
1
1
1
1
4
```

### Output 1

```
1
```

### Explicación 1

Las cartas son `1, 1, 1, 1` y el objetivo es `4`. Una combinación válida que utiliza las cuatro cartas:

$$1 + 1 + 1 + 1 = 4$$

Resultado: **1**.

---

### Input 2

```
4
1
2
3
4
99
```

### Output 2

```
0
```

### Explicación 2

Las cartas son `1, 2, 3, 4` y el objetivo es `99`. No existe ninguna combinación de las cuatro cartas con las operaciones `+`, `-`, `*`, `/` que dé como resultado $99$. Resultado: **0**.

---

### Input 3

```
3
6
3
2
4
```

### Output 3

```
1
```

### Explicación 3

Las cartas son `6, 3, 2` y el objetivo es `4`. Una combinación válida:

| Paso | Operación   | Cartas restantes |
| ---- | ----------- | ---------------- |
| 1    | $6 / 3 = 2$ | `2, 2`           |
| 2    | $2 * 2 = 4$ | `4`              |

Se utilizan las tres cartas y se alcanza el objetivo. Resultado: **1**.

---

### Input 4

```
5
3
8
2
1
5
24
```

### Output 4

```
1
```

### Explicación 4

Las cartas son `3, 8, 2, 1, 5` y el objetivo es `24`. Una combinación válida:

| Paso | Operación        | Cartas restantes |
| ---- | ---------------- | ---------------- |
| 1    | $8 / 2 = 4$      | `3, 4, 1, 5`     |
| 2    | $5 - 1 = 4$      | `3, 4, 4`        |
| 3    | $4 + 4 = 8$      | `3, 8`           |
| 4    | $3 \cdot 8 = 24$ | `24`             |

Se utilizan las cinco cartas y se alcanza el objetivo. Resultado: **1**.
