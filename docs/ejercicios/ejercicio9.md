# Ejercicio 9 - Campamento dinámico

## Descripción

Un amigo decidió organizar un campamento de varios días en una zona remota, lejos de la civilización, y te invitó a ser parte de la aventura. Como suele pasar, nadie quiere cargar peso de más… pero tampoco quieren olvidarse de nada importante.

Antes de partir, se reúnen para decidir qué objetos llevar. Tienen una lista de $n$ objetos disponibles, y cada uno puede elegirse a lo sumo una vez.

Cada objeto está identificado por un id único, que no necesariamente guarda relación con su posición en la entrada.

De cada objeto se conoce:

- su id,
- su nombre,
- su peso,
- su volumen,
- su costo,
- su valor de utilidad para la expedición,
- y su categoría, que puede ser `supervivencia` o `comida`.

La mochila tiene restricciones logísticas estrictas. La selección final de objetos no puede exceder:

- un peso máximo $P$,
- un volumen máximo $V$,
- un costo máximo $C$.

Además, decidieron que iban a probar sus habilidades en la naturaleza limitando la cantidad de objetos que pueden llevar de cada categoría a lo sumo a:

- $S$ objetos de categoría `supervivencia`,
- $M$ objetos de categoría `comida`.

Entre todas las selecciones válidas, se debe elegir aquella que:

1. maximice el valor total de utilidad;
2. en caso de empate en el valor total, minimice el peso total.

Si no existe ninguna selección que cumpla simultáneamente todas las restricciones, debe indicarse explícitamente.

---

## Entrada

- La primera línea contiene un entero positivo $n$ ($1 \leq n \leq 200$), la cantidad de objetos disponibles.
- La segunda línea contiene cinco enteros positivos $P$, $V$, $C$, $S$ y $M$ ($1 \leq P, V, C \leq 200$, $0 \leq S, M \leq n$), donde:

  - $P$ es el peso máximo permitido,
  - $V$ es el volumen máximo permitido,
  - $C$ es el costo máximo permitido,
  - $S$ es la cantidad máxima de objetos de supervivencia permitida,
  - $M$ es la cantidad máxima de objetos de comida permitida.

- Las siguientes $n$ líneas describen los objetos. Cada una contiene:

```
id nombre peso volumen costo valor categoria
```

donde:

- $1891 \leq id \leq 10^6$,
- todos los ids son distintos,
- `nombre` es una cadena sin espacios,
- `peso`, `volumen`, `costo` y `valor` son enteros positivos,
- `categoria` es la cadena `supervivencia` o `comida`.

**Importante:** el orden de procesamiento de los objetos en la programación dinámica debe respetar el orden en que los objetos aparecen en la entrada.

---

## Salida

Si existe una solución válida, imprimir:

- en la primera línea, dos enteros: el valor total máximo alcanzado y el peso total de una solución óptima;
- en la segunda línea, un entero $k$: la cantidad de objetos seleccionados;
- luego $k$ líneas, cada una con el nombre de un objeto elegido, en orden creciente de id.

Si no existe ninguna solución válida, imprimir únicamente:

```
Imposible
```

---

## Restricciones

- Resolver utilizando tabulación.
- La solución debe contemplar simultáneamente las restricciones de peso, volumen, costo y cantidades máximas por categoría.
- El criterio de comparación entre dos soluciones debe ser:
  - mayor valor total;
  - en caso de empate, menor peso total.
- La reconstrucción de la solución óptima debe realizarse a partir de la tabla de programación dinámica.
- Para imprimir los objetos seleccionados en orden creciente de id, deberá utilizarse una estructura de datos adecuada.

---

## Ejemplo

### Input

```
5
10 12 11 2 2
5001 cuerda 3 2 4 8 supervivencia
3200 linterna 2 2 3 6 supervivencia
8700 galletitas 2 3 2 5 comida
4100 arroz 3 4 3 7 comida
9200 manta 4 3 5 9 supervivencia
```

### Output

```
21 8
3
linterna
arroz
cuerda
```

---

## Explicación

Una selección válida es:

- 3200 linterna: peso 2, volumen 2, costo 3, valor 6, supervivencia  
- 4100 arroz: peso 3, volumen 4, costo 3, valor 7, comida  
- 5001 cuerda: peso 3, volumen 2, costo 4, valor 8, supervivencia  

Totales:

- peso = 8  
- volumen = 8  
- costo = 10  
- valor = 21  

Se cumple:

- peso $\leq 10$  
- volumen $\leq 12$  
- costo $\leq 11$  
- a lo sumo 2 objetos de supervivencia  
- a lo sumo 2 objetos de comida  

No existe otra selección válida con mayor valor total.

Los objetos se imprimen ordenados por id creciente: $3200 < 4100 < 5001$.
