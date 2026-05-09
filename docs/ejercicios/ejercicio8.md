# Ejercicio 8 - El cartel de neón

## Descripción

Una tienda de letras luminosas recibe un pedido especial: un cliente quiere armar un cartel de neón usando exactamente
las letras que tiene disponibles (representadas como una cadena de letras latinas minúsculas). El único requisito del
cliente es que **ninguna letra del cartel puede quedar al lado de otra letra igual**, ya que esto genera un
cortocircuito en el cableado de neón.

De todas las formas posibles de organizar las letras que cumplan esa condición, el cliente quiere la que se lea como la
**palabra lexicográficamente mayor** (es decir, la que aparecería última en un diccionario).

Dada la cadena de letras disponibles, determine la organización lexicográficamente mayor tal que no haya dos letras
iguales adyacentes.

## Entrada

- Una única línea con una cadena $S$ de letras latinas minúsculas ($1 \leq |S| \leq 10^6$).

## Salida

- Una única línea con la reorganización lexicográficamente mayor de $S$ tal que no haya dos caracteres iguales
  adyacentes.
- Si no es posible, imprima `Imposible`.

## Restricciones

- Resolver usando una **estrategia greedy**.
- **Tiempo**: $O(N)$ donde $N = |S|$, considerando el alfabeto de 26 letras como constante.
- **Espacio**: $O(N)$.

## Ejemplo

### Input 1

```
aab
```

### Output 1

```
aba
```

### Explicación 1

Las letras disponibles son: `a`, `a`, `b`. Las posibles reorganizaciones son:

| Reorganización | ¿Válida?                  |
|----------------|---------------------------|
| `aab`          | No (`a` y `a` adyacentes) |
| `aba`          | Sí                        |
| `baa`          | No (`a` y `a` adyacentes) |

La única reorganización válida es `aba`. Resultado: **aba**.

---

### Input 2

```
aaabbc
```

### Output 2

```
cababa
```

### Explicación 2

Letras disponibles: 3 `a`, 2 `b`, 1 `c`. La cadena `cababa` no tiene letras adyacentes iguales y es la mayor lexicográfica entre las reorganizaciones válidas. Alternativas lex mayores como `ccbbaa` o `cbabaa` quedan descartadas por tener repeticiones adyacentes.

---

### Input 3

```
aaa
```

### Output 3

```
Imposible
```

### Explicación 3

Letras disponibles: 3 `a`. Para que tres `a` no queden adyacentes hacen falta al menos dos letras de relleno entre ellas (algo como `a?a?a`). Como no hay otras letras disponibles, no existe ninguna reorganización válida.

---

### Input 4

```
abcabc
```

### Output 4

```
cbcaba
```

### Explicación 4

Letras disponibles: 2 `a`, 2 `b`, 2 `c`. La cadena `cbcaba` no tiene adyacencias iguales y es la mayor lexicográfica entre las válidas. Reorganizaciones lex mayores como `ccbbaa` o `cbcbaa` quedan descartadas por sus repeticiones adyacentes.