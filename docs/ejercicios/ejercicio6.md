# Ejercicio 6 - Monitoreo de focos críticos

## Descripción

Una región contiene varios focos de radiación activos, cada uno ubicado en una posición del plano descrita por coordenadas cartesianas $(x, y)$. Un par de focos se considera **crítico** cuando la distancia euclídea entre ellos es menor o igual a un umbral $D$, ya que en ese caso pueden superponer sus dosis y requerir intervención inmediata.

Dado el conjunto de focos detectados, determine si existe al menos un par crítico.

La distancia entre dos focos $(x_1, y_1)$ y $(x_2, y_2)$ se calcula como:

$$
\sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}
$$

## Entrada

- La primera línea contiene dos enteros $N$ y $D$ ($1 \leq N \leq 10^6$, $0 \leq D \leq 10^9$): la cantidad de focos detectados y la distancia umbral, respectivamente.
- Las siguientes $N$ líneas contienen las coordenadas $x$ e $y$ de cada foco ($-10^9 \leq x, y \leq 10^9$).
- Los focos se listan en **orden arbitrario** y puede haber dos o más focos en la misma posición.

## Salida

Imprima una única línea con `true` si existe al menos un par crítico, o `false` en caso contrario.

## Restricciones

- Resolver utilizando una estrategia de **Divide and Conquer**.
- Complejidad esperada: $O(N \log N)$ en el peor caso.

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

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 320" width="360" style="max-width:100%;height:auto;display:block;margin:16px 0">
  <style>
    .ax { stroke: #888; stroke-width: 1; fill: none; }
    .grid { stroke: #eee; stroke-width: 1; }
    .tl { font: 11px sans-serif; fill: #555; }
    .pt { fill: #4a90d9; }
    .pl { font: 11px sans-serif; fill: #333; }
    .crit { stroke: #e74c3c; stroke-width: 2; }
    .cl { font: 11px sans-serif; fill: #e74c3c; }
  </style>
  <line class="grid" x1="155" y1="290" x2="155" y2="40"/>
  <line class="grid" x1="280" y1="290" x2="280" y2="40"/>
  <line class="grid" x1="30" y1="165" x2="280" y2="165"/>
  <line class="grid" x1="30" y1="40" x2="280" y2="40"/>
  <line class="ax" x1="30" y1="290" x2="290" y2="290"/>
  <line class="ax" x1="30" y1="290" x2="30" y2="35"/>
  <text class="tl" x="30" y="306" text-anchor="middle">0</text>
  <text class="tl" x="155" y="306" text-anchor="middle">5</text>
  <text class="tl" x="280" y="306" text-anchor="middle">10</text>
  <text class="tl" x="22" y="294" text-anchor="end">0</text>
  <text class="tl" x="22" y="169" text-anchor="end">5</text>
  <text class="tl" x="22" y="44" text-anchor="end">10</text>
  <line class="crit" x1="30" y1="290" x2="55" y2="265"/>
  <text class="cl" x="80" y="278">d = √2 ≤ 2</text>
  <circle class="pt" cx="30" cy="290" r="4"/>
  <circle class="pt" cx="55" cy="265" r="4"/>
  <text class="pl" x="63" y="258">(1,1)</text>
  <circle class="pt" cx="130" cy="190" r="4"/>
  <text class="pl" x="138" y="187">(4,4)</text>
  <circle class="pt" cx="205" cy="115" r="4"/>
  <text class="pl" x="213" y="112">(7,7)</text>
  <circle class="pt" cx="280" cy="40" r="4"/>
  <text class="pl" x="272" y="55" text-anchor="end">(10,10)</text>
</svg>

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

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 320" width="360" style="max-width:100%;height:auto;display:block;margin:16px 0">
  <style>
    .ax { stroke: #888; stroke-width: 1; fill: none; }
    .grid { stroke: #eee; stroke-width: 1; }
    .tl { font: 11px sans-serif; fill: #555; }
    .pt { fill: #4a90d9; }
    .pl { font: 11px sans-serif; fill: #333; }
  </style>
  <line class="grid" x1="155" y1="290" x2="155" y2="40"/>
  <line class="grid" x1="280" y1="290" x2="280" y2="40"/>
  <line class="grid" x1="30" y1="165" x2="280" y2="165"/>
  <line class="grid" x1="30" y1="40" x2="280" y2="40"/>
  <line class="ax" x1="30" y1="290" x2="290" y2="290"/>
  <line class="ax" x1="30" y1="290" x2="30" y2="35"/>
  <text class="tl" x="30" y="306" text-anchor="middle">0</text>
  <text class="tl" x="155" y="306" text-anchor="middle">5</text>
  <text class="tl" x="280" y="306" text-anchor="middle">10</text>
  <text class="tl" x="22" y="294" text-anchor="end">0</text>
  <text class="tl" x="22" y="169" text-anchor="end">5</text>
  <text class="tl" x="22" y="44" text-anchor="end">10</text>
  <circle class="pt" cx="30" cy="290" r="4"/>
  <text class="pl" x="38" y="285">(0,0)</text>
  <circle class="pt" cx="105" cy="215" r="4"/>
  <text class="pl" x="113" y="212">(3,3)</text>
  <circle class="pt" cx="180" cy="140" r="4"/>
  <text class="pl" x="188" y="137">(6,6)</text>
  <circle class="pt" cx="255" cy="65" r="4"/>
  <text class="pl" x="247" y="55" text-anchor="end">(9,9)</text>
</svg>

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

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 320" width="360" style="max-width:100%;height:auto;display:block;margin:16px 0">
  <style>
    .ax { stroke: #888; stroke-width: 1; fill: none; }
    .grid { stroke: #eee; stroke-width: 1; }
    .tl { font: 11px sans-serif; fill: #555; }
    .pt { fill: #4a90d9; }
    .pl { font: 11px sans-serif; fill: #333; }
    .crit-pt { fill: #e74c3c; }
    .cl { font: 11px sans-serif; fill: #e74c3c; }
  </style>
  <line class="grid" x1="155" y1="290" x2="155" y2="40"/>
  <line class="grid" x1="280" y1="290" x2="280" y2="40"/>
  <line class="grid" x1="30" y1="165" x2="280" y2="165"/>
  <line class="grid" x1="30" y1="40" x2="280" y2="40"/>
  <line class="ax" x1="30" y1="290" x2="290" y2="290"/>
  <line class="ax" x1="30" y1="290" x2="30" y2="35"/>
  <text class="tl" x="30" y="306" text-anchor="middle">0</text>
  <text class="tl" x="155" y="306" text-anchor="middle">5</text>
  <text class="tl" x="280" y="306" text-anchor="middle">10</text>
  <text class="tl" x="22" y="294" text-anchor="end">0</text>
  <text class="tl" x="22" y="169" text-anchor="end">5</text>
  <text class="tl" x="22" y="44" text-anchor="end">10</text>
  <circle class="crit-pt" cx="153" cy="167" r="4"/>
  <circle class="crit-pt" cx="157" cy="163" r="4"/>
  <text class="cl" x="165" y="160">(5,5) ×2 — d = 0</text>
  <circle class="pt" cx="280" cy="40" r="4"/>
  <text class="pl" x="272" y="55" text-anchor="end">(10,10)</text>
</svg>

Existen dos focos en exactamente la misma posición, por lo que la distancia entre ellos es $0$.
