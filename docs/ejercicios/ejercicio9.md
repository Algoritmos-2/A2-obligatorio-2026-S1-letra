# Ejercicio 9 - Campamento dinámico

## Descripción

Un amigo decidió organizar un campamento de varios días en una zona remota, lejos de la civilización, y te invitó a ser parte de la aventura. Como suele pasar, nadie quiere cargar peso de más… pero tampoco quieren olvidarse de nada importante.

Antes de partir, se reúnen para decidir qué objetos llevar. Tienen una lista de $n$ objetos disponibles, y cada uno puede elegirse a lo sumo una vez. Cada objeto tiene un peso, un volumen, un costo, un valor de utilidad y una categoría (`supervivencia` o `comida`).

La mochila tiene restricciones logísticas estrictas: la selección final no puede exceder un peso máximo $P$, un volumen máximo $V$, ni un costo máximo $C$. Además, para probar sus habilidades en la naturaleza, se limita la cantidad de objetos por categoría: a lo sumo $S$ de `supervivencia` y $M$ de `comida`.

Entre todas las selecciones válidas (incluyendo la **mochila vacía**, que siempre cumple las restricciones con valor y peso cero), se debe elegir aquella que:

1. maximice el valor total de utilidad;
2. en caso de empate, minimice el peso total;
3. en caso de empate, minimice la cantidad de objetos seleccionados.

## Entrada

- La primera línea contiene un entero $n$ ($1 \leq n \leq 35$), la cantidad de objetos disponibles.
- La segunda línea contiene cinco enteros $P$, $V$, $C$, $S$ y $M$ ($1 \leq P, V, C \leq 20$, $0 \leq S, M \leq 15$): el peso máximo, el volumen máximo, el costo máximo, la cantidad máxima de objetos de supervivencia y la cantidad máxima de objetos de comida, respectivamente.
- Las siguientes $n$ líneas describen un objeto cada una, con el formato:

  ```
  peso volumen costo valor categoria
  ```

  donde $1 \leq peso, volumen, costo, valor \leq 100$, y `categoria` es la cadena `supervivencia` o `comida`.

## Salida

Imprima en una única línea tres enteros separados por espacio: el valor total máximo alcanzado, el peso total y la cantidad de objetos seleccionados de la solución óptima. Si la mejor solución es la mochila vacía, los tres valores son `0`.

## Restricciones

- Resolver utilizando tabulación.
- La solución debe contemplar simultáneamente las restricciones de peso, volumen, costo y cantidades máximas por categoría.

## Ejemplo

### Input

```
5
10 12 11 2 2
3 2 4 8 supervivencia
2 2 3 6 supervivencia
2 3 2 5 comida
3 4 3 7 comida
4 3 5 9 supervivencia
```

### Output

```
22 9 3
```

### Explicación

Una selección válida es:

- objeto 2 (linterna): peso 2, volumen 2, costo 3, valor 6, supervivencia
- objeto 4 (arroz): peso 3, volumen 4, costo 3, valor 7, comida
- objeto 5 (manta): peso 4, volumen 3, costo 5, valor 9, supervivencia

Totales: peso 9, volumen 9, costo 11, valor 22. Se cumple peso $\leq 10$, volumen $\leq 12$, costo $\leq 11$, y hay a lo sumo 2 objetos de cada categoría. No existe otra selección con mayor valor total. La salida es `22 9 3`: valor 22, peso 9, 3 objetos.
