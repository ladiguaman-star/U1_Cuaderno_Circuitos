# Semana 4: Ejercicios

**Tema:** Circuitos aritméticos

> **Indicaciones:** En los ejercicios de suma y resta escriba el acarreo de cada columna. Para los circuitos, deduzca las expresiones desde la tabla de verdad y el mapa de Karnaugh en lugar de recordarlas. Considere 4 bits en complemento a dos salvo que se indique lo contrario.

---

## Bloque A. Suma binaria

**Ejercicio 4.1.** Sume $1011 + 0110$ escribiendo el acarreo de cada columna. Interprete el resultado en decimal.

**Ejercicio 4.2.** Sume $0111 + 0111$. Indique el resultado interpretado (a) sin signo y (b) con signo. ¿Es correcto en cada caso?

---

## Bloque B. Diseño del semisumador y del sumador completo

**Ejercicio 4.3 (Semisumador).**

a) Construya la tabla de verdad con entradas $A, B$ y salidas $S, C$.
b) Deduzca las expresiones de $S$ y $C$ y reconozca las compuertas.
c) Indique cuántas compuertas y circuitos integrados requiere (considere los CI 7486 y 7408).

**Ejercicio 4.4 (Sumador completo).**

a) Construya la tabla de verdad de $A, B, C_{in}$ contando el número de unos y escribiéndolo como $C_{out}\,S$.
b) Dibuje los mapas de Karnaugh de $S$ y de $C_{out}$ (columnas $AB$, fila $C_{in}$) y obtenga las expresiones mínimas.
c) Implemente $C_{out}$ en las formas $AB + AC_{in} + BC_{in}$ y $AB + C_{in}(A \oplus B)$. Compare el número de compuertas de cada sumador completo y estime los CI de un sumador de 4 bits con compuertas sueltas.

**Ejercicio 4.5 (Demostración).** Complete la tabla etapa por etapa para $0110 + 0111$ con cuatro sumadores completos:

| Etapa | $A$ | $B$ | $C_{in}$ | N.º de 1 | $S$ | $C_{out}$ |
|:-----:|:---:|:---:|:--------:|:--------:|:---:|:---------:|
| 0     |     |     |          |          |     |           |
| 1     |     |     |          |          |     |           |
| 2     |     |     |          |          |     |           |
| 3     |     |     |          |          |     |           |

---

## Bloque C. Retardo de propagación

**Ejercicio 4.6.** Suponga que cada compuerta tarda 10 ns y que el acarreo cruza 2 compuertas por etapa.

a) Estime el retardo de un sumador *ripple* de 16 bits (también de 8 y de 32 bits).
b) Si el sistema debe entregar el resultado en un máximo de 200 ns, ¿cuál es el máximo número de bits del sumador?

---

## Bloque D. Resta con el sumador

**Ejercicio 4.7.** Restar $0110 - 0011$ con el sumador (con $M = 1$). Muestre $B$, $\overline{B}$, el $+1$ aportado por $C_{in}$ y el resultado.

**Ejercicio 4.8.** Efectúe $0101 - 0111$ con el sumador/restador. Interprete el resultado y el acarreo de salida.

---

## Bloque E. Desbordamiento

**Ejercicio 4.9.** Para cada suma de 4 bits en complemento a dos, calcule $S$, $C_{out}$, $C_3$ y $V = C_3 \oplus C_4$, e indique si hay desbordamiento:

a) $0101 + 0100$
b) $1011 + 1010$
c) $1110 + 0011$

> **Pregunta de reflexión:** en el caso (c), ¿por qué $C_{out} = 1$ no implica error?

---

## Bloque F. Comparador de magnitud

**Ejercicio 4.10.** Compare $A = 10$ y $B = 01$ (2 bits). ¿$A > B$? ¿$A = B$?

**Ejercicio 4.11.** Compare, con las expresiones de 2 bits, los pares (a) $A = 11,\ B = 10$ y (b) $A = 01,\ B = 01$.

**Ejercicio 4.12.** Diseñe un comparador de igualdad de 4 bits con compuertas XNOR y AND. Indique cuántas compuertas requiere.

---

[← Anterior: Resumen](./resumen.md) | [Siguiente: Soluciones →](./soluciones.md)
