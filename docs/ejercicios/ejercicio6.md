# Ejercicio 6 - Monitoreo de focos críticos

## Descripción

En una región se han detectado múltiples focos activos que emiten radiación. Cada foco se encuentra ubicado en una posición del plano representada por sus coordenadas cartesianas.

Dos focos se consideran **críticos** si la distancia entre ellos es menor o igual a un valor umbral $D$. La presencia de focos críticos puede implicar superposición de dosis y requiere intervención inmediata.

Dado el conjunto de focos detectados, determine si existe al menos un par de focos críticos en la región.

---

## Entrada

- La primera línea contiene dos valores $N$ y $D$ ($1 \leq N \leq 2 \cdot 10^5$, $0 \leq D \leq 10^9$), donde:
  - $N$ es la cantidad de focos detectados.
  - $D$ es la distancia umbral.

- Las siguientes $N$ líneas contienen dos números $x$ e $y$, que representan las coordenadas de cada foco.

- Se garantiza que los focos están **ordenados de forma creciente según su coordenada $x$**.

---

## Salida

Imprima:

```
true
```

si existe al menos un par de focos cuya distancia sea menor o igual a $D$.

En caso contrario, imprima:

```
false
```

---

## Restricciones

- Resolver utilizando una estrategia de **Divide and Conquer**.
- Complejidad esperada: $O(N \log N)$ en el peor caso.
- No se permite utilizar soluciones de complejidad cuadrática.
- Las coordenadas pueden ser negativas.
- Puede haber focos en la misma posición.

---

## Aclaraciones

La distancia entre dos focos $(x_1, y_1)$ y $(x_2, y_2)$ se define como:

$$
\sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}
$$

Para evitar errores de precisión, se recomienda trabajar con distancias al cuadrado.

---

## Ejemplo

### Input 1

```
5 2
0 0
1 1
4 4
7 7
10 10
```

### Output 1

```
true
```

### Explicación 1

Los focos en $(0,0)$ y $(1,1)$ están a distancia $\sqrt{2}$, que es menor que $2$.

---

### Input 2

```
4 1
0 0
3 3
6 6
9 9
```

### Output 2

```
false
```

### Explicación 2

Todos los focos están separados por distancias mayores que $1$.

---

### Input 3

```
3 0
5 5
5 5
10 10
```

### Output 3

```
true
```

### Explicación 3

Existen dos focos en exactamente la misma posición, por lo que la distancia entre ellos es $0$.
