# Ejercicio 1 - Acceso al laboratorio

## Descripción

Un investigador necesita atravesar un edificio universitario compuesto por $n$ salas dispuestas en línea y numeradas de $1$ a $n$. El investigador comienza en la sala $1$ y debe llegar a la sala $n$, donde se encuentra el servidor central con los resultados de su investigación.

Para pasar de la sala $x$ a la sala $x+1$, debe abrir la puerta que las conecta usando la llave correspondiente.

Existen varios tipos de puertas, representadas por **letras latinas mayúsculas**, y varios tipos de llaves, representadas por **letras latinas minúsculas**. Una llave de tipo $t$ puede abrir una puerta de tipo $T$ si y solo si $t$ y $T$ son la misma letra (una en minúscula y otra en mayúscula). Por ejemplo, la llave `f` abre la puerta `F`.

Cada una de las primeras $n - 1$ salas contiene exactamente una llave de algún tipo. Una vez que el investigador usa una llave para abrir una puerta, la deja insertada en la cerradura y avanza a la siguiente sala. Es decir, **cada llave solo puede usarse una vez**.

El investigador se da cuenta de que podría quedar atrapado en alguna sala sin la llave necesaria para la siguiente puerta. Antes de comenzar el recorrido, puede solicitar a la administración del edificio cualquier cantidad de llaves adicionales de cualquier tipo.

Dado el plano del edificio, determine la **cantidad mínima de llaves adicionales** que el investigador necesita solicitar para garantizar que pueda llegar desde la sala $1$ hasta la sala $n$.

## Entrada

- La primera línea contiene un entero positivo $n$ ($2 \leq n \leq 10^7$), la cantidad de salas del edificio.
- La segunda línea contiene una cadena $s$ de longitud $2n - 2$.

Las posiciones **impares** de la cadena contienen letras latinas minúsculas: los tipos de llaves que se encuentran en las salas correspondientes.

Las posiciones **pares** de la cadena contienen letras latinas mayúsculas: los tipos de puertas entre las salas consecutivas.

## Salida

Imprima un único número entero: la cantidad mínima de llaves adicionales que el investigador necesita solicitar para ir de la sala $1$ a la sala $n$.

## Restricciones

- Utilizar una **tabla de hash** o alguna **técnica de hashing** para resolver el problema.
- Resolver en orden temporal: $O(N)$ en el peor caso, siendo $N$ la cantidad de salas.

## Ejemplo

### Input 1

```
3
aAbB
```

### Output 1

```
0
```

### Explicación 1

El edificio tiene $3$ salas y la cadena es `aAbB`.

| Sala | Llave encontrada | Puerta siguiente | Acción                                 |
| ---- | ---------------- | ---------------- | -------------------------------------- |
| 1    | `a`              | `A`              | Usa la llave `a` que acaba de recoger. |
| 2    | `b`              | `B`              | Usa la llave `b` que acaba de recoger. |

Todas las llaves coinciden con sus puertas inmediatas. No necesita solicitar ninguna llave adicional. Respuesta: **0**.

---

### Input 2

```
4
aBaCaB
```

### Output 2

```
3
```

### Explicación 2

El edificio tiene $4$ salas y la cadena es `aBaCaB`.

| Sala | Llave encontrada | Puerta siguiente | Llaves disponibles | Acción                                  |
| ---- | ---------------- | ---------------- | ------------------ | --------------------------------------- |
| 1    | `a`              | `B`              | {`a`:1}            | No tiene `b`. **Solicita 1 llave** `b`. |
| 2    | `a`              | `C`              | {`a`:2}            | No tiene `c`. **Solicita 1 llave** `c`. |
| 3    | `a`              | `B`              | {`a`:3}            | No tiene `b`. **Solicita 1 llave** `b`. |

El investigador siempre recoge llaves de tipo `a`, pero nunca las necesita. Debe solicitar cada llave que requiere. Respuesta: **3**.

---

### Input 3

```
5
xYyXzZaZ
```

### Output 3

```
2
```

### Explicación 3

El edificio tiene $5$ salas y la cadena es `xYyXzZaZ`.

| Sala | Llave encontrada | Puerta siguiente | Llaves disponibles | Acción                                  |
| ---- | ---------------- | ---------------- | ------------------ | --------------------------------------- |
| 1    | `x`              | `Y`              | {`x`:1}            | No tiene `y`. **Solicita 1 llave** `y`. |
| 2    | `y`              | `X`              | {`x`:1, `y`:1}     | Usa `x` (recogida en sala 1).           |
| 3    | `z`              | `Z`              | {`y`:1}            | Usa `z` que acaba de recoger.           |
| 4    | `a`              | `Z`              | {`y`:1, `a`:1}     | No tiene `z`. **Solicita 1 llave** `z`. |

La llave `y` recogida en la sala 2 nunca se usa. Respuesta: **2**.

---

### Input 4

```
7
aAbCcBdDeFfE
```

### Output 4

```
2
```

### Explicación 4

El edificio tiene $7$ salas y la cadena es `aAbCcBdDeFfE`. Este ejemplo ilustra los tres escenarios posibles:

| Sala | Llave encontrada | Puerta siguiente | Llaves disponibles    | Acción                                                  |
| ---- | ---------------- | ---------------- | --------------------- | ------------------------------------------------------- |
| 1    | `a`              | `A`              | {`a`:1}               | **Coincidencia directa**: usa `a` que acaba de recoger. |
| 2    | `b`              | `C`              | {`b`:1}               | No tiene `c`. **Solicita 1 llave** `c`.                 |
| 3    | `c`              | `B`              | {`b`:1, `c`:1}        | **Usa llave guardada**: usa `b` (recogida en sala 2).   |
| 4    | `d`              | `D`              | {`c`:1, `d`:1}        | **Coincidencia directa**: usa `d` que acaba de recoger. |
| 5    | `e`              | `F`              | {`c`:1, `e`:1}        | No tiene `f`. **Solicita 1 llave** `f`.                 |
| 6    | `f`              | `E`              | {`c`:1, `e`:1, `f`:1} | **Usa llave guardada**: usa `e` (recogida en sala 5).   |
