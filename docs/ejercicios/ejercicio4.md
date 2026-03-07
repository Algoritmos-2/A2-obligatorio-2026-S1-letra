# Ejercicio 4 - Interconexiones planetarias

## Descripción

En una galaxia con múltiples sistemas planetarios, los planetas están interconectados por portales espaciales bidireccionales. Cada portal conecta dos planetas y tiene un costo de energía asociado para viajar a través de él.

Dado un mapa de la galaxia, determine la **cantidad mínima de energía** requerida para viajar desde un planeta de origen a un planeta de destino utilizando los portales disponibles.

Los planetas se identifican por su **nombre** (una cadena de caracteres). La tabla de hash se utiliza únicamente para traducir los nombres de los planetas a índices numéricos. El resultado se obtiene de ejecutar el algoritmo de camino más corto sobre el grafo construido.

## Entrada

- La primera línea contiene dos enteros $N$ y $M$ ($1 \leq N \leq 10^5$, $0 \leq M \leq 10^5$), la cantidad de planetas y la cantidad de portales, respectivamente.
- Las siguientes $M$ líneas contienen dos cadenas $A$ y $B$ y un entero $C$ ($1 \leq C \leq 10^6$), que representan un portal bidireccional entre el planeta $A$ y el planeta $B$ con un costo de energía $C$. No existen costos negativos.
- La última línea contiene dos cadenas $O$ y $D$, que representan el planeta de origen y el planeta de destino.

Los nombres de los planetas son cadenas de letras latinas minúsculas con longitud entre 1 y 20.

## Salida

Imprima la cantidad mínima de energía requerida para viajar desde el planeta de origen al planeta de destino. Si no es posible llegar, imprima `-1`.

## Restricciones

- Utilizar el algoritmo de **Dijkstra** para resolver el problema.
- Utilizar una **tabla de hash** para mapear los nombres de los planetas a índices numéricos.
- Resolver en orden temporal: $O((M + N) \log N)$ en el peor caso.

## Ejemplo

### Input 1

```
5 6
terra nova 10
nova centro 5
centro lejano 20
lejano borde 10
terra centro 30
centro borde 15
terra borde
```

### Output 1

```
30
```

### Explicación 1

Planetas: terra, nova, centro, lejano, borde.

```cytoscape
{"nodes": ["terra", "nova", "centro", "lejano", "borde"], "edges": [["terra","nova",10],["nova","centro",5],["centro","lejano",20],["lejano","borde",10],["terra","centro",30],["centro","borde",15]]}
```

Caminos posibles de terra a borde:
- terra → nova → centro → borde: $10 + 5 + 15 = 30$
- terra → centro → borde: $30 + 15 = 45$
- terra → nova → centro → lejano → borde: $10 + 5 + 20 + 10 = 45$

El camino mínimo cuesta **30**.

---

### Input 2

```
3 1
alfa beta 5
alfa gamma
```

### Output 2

```
-1
```

### Explicación 2

```cytoscape
{"nodes": ["alfa", "beta", "gamma"], "edges": [["alfa","beta",5]]}
```

Solo existe un portal entre alfa y beta. No hay forma de llegar de alfa a gamma. Resultado: **-1**.

---

### Input 3

```
4 5
sol luna 3
sol marte 7
luna marte 1
luna jupiter 10
marte jupiter 2
sol jupiter
```

### Output 3

```
6
```

### Explicación 3

```cytoscape
{"nodes": ["sol", "luna", "marte", "jupiter"], "edges": [["sol","luna",3],["sol","marte",7],["luna","marte",1],["luna","jupiter",10],["marte","jupiter",2]]}
```

Caminos de sol a jupiter:
- sol → luna → jupiter: $3 + 10 = 13$
- sol → marte → jupiter: $7 + 2 = 9$
- sol → luna → marte → jupiter: $3 + 1 + 2 = 6$

El camino mínimo cuesta **6** (pasando por luna y marte).

---

### Input 4

```
6 7
alpha beta 4
alpha gamma 2
beta delta 5
gamma beta 1
gamma epsilon 10
delta zeta 2
epsilon zeta 7
alpha zeta
```

### Output 4

```
10
```

### Explicación 4

```cytoscape
{"nodes": ["alpha", "beta", "gamma", "delta", "epsilon", "zeta"], "edges": [["alpha","beta",4],["alpha","gamma",2],["beta","delta",5],["gamma","beta",1],["gamma","epsilon",10],["delta","zeta",2],["epsilon","zeta",7]]}
```

Ejecución de Dijkstra desde alpha:

| Paso | Planeta procesado | Distancia acumulada | Vía           |
| ---- | ----------------- | ------------------- | ------------- |
| 1    | alpha             | 0                   | origen        |
| 2    | gamma             | 2                   | alpha         |
| 3    | beta              | 3                   | gamma         |
| 4    | delta             | 8                   | beta          |
| 5    | zeta              | 10                  | delta         |
| 6    | epsilon           | 12                  | gamma         |

El camino más corto es alpha → gamma → beta → delta → zeta con costo **10**.