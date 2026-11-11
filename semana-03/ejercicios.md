# Semana 3: Ejercicios

**Tema:** Mapas de Karnaugh, condiciones indiferentes y universalidad NAND/NOR

> **Indicaciones:** Para cada problema dibuje el mapa, marque los grupos, justifique cada agrupación (¿es primo?, ¿es esencial?) y escriba la expresión mínima. Cuando se solicite, calcule el costo en literales, compuertas y circuitos integrados (CI).

---

## Bloque A. Mapas de Karnaugh en SOP

**Ejercicio 3.1 (T1).** Simplifique $F(A,B,C) = \Sigma m(1, 3, 4, 6)$. ¿Reconoce la función resultante como alguna compuerta conocida?

**Ejercicio 3.2 (T2).** Simplifique $F(A,B,C,D) = \Sigma m(0, 1, 4, 5, 6, 7, 14, 15)$.

> **Pista:** ¿algún implicante primo sobra? Identifique los primos esenciales antes de elegir los restantes.

**Ejercicio 3.3 (T3).** Simplifique $F(A,B,C,D) = \Sigma m(0, 2, 5, 8, 10, 13)$.

> **Pista:** atención a las esquinas.

**Ejercicio 3.4 (Ticket de salida).** Simplifique en SOP mínima $F(A,B,C,D) = \Sigma m(0, 2, 5, 7, 8, 10, 13, 15)$ y reconozca la compuerta equivalente.

---

## Bloque B. Diagnóstico de errores

**Ejercicio 3.5 (T4).** Un estudiante entregó el siguiente mapa para $F = \Sigma m(0, 1, 4, 5, 6, 7, 14, 15)$:

| $AB \backslash CD$ | 00 | 01 | 10 | 11 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 1  | 0  | 0  |
| **01**             | 1  | 1  | 1  | 1  |
| **11**             | 0  | 0  | 1  | 1  |
| **10**             | 0  | 0  | 0  | 0  |

y obtuvo:

$$
F = \overline{A}\,\overline{C} + BC + \overline{A}B + \overline{A}\,\overline{B}\,\overline{C}
$$

Encuentre **tres errores**, explique cada uno y escriba la expresión correcta.

---

## Bloque C. Mapas en POS

**Ejercicio 3.6.** Obtenga la POS mínima de $F(A,B,C) = \Sigma m(1, 3, 4, 6)$ (agrupando los 0) y compárela con la SOP del ejercicio 3.1.

**Ejercicio 3.7.** Para $F(A,B,C,D) = \Sigma m(0, 1, 2, 5, 8, 9, 10)$, verifique que $F = (\overline{A} + \overline{B})(\overline{B} + D)(\overline{C} + \overline{D})$ listando las celdas con 0 que cubre cada suma.

---

## Bloque D. Condiciones indiferentes

**Ejercicio 3.8.** Un dígito BCD llega a un circuito que debe indicar si es **par** (incluyendo el 0).
$F(A,B,C,D) = \Sigma m(0, 2, 4, 6, 8) + d(10, 11, 12, 13, 14, 15)$. Obtenga la SOP mínima.

**Ejercicio 3.9.** Un dígito BCD debe detectarse como **múltiplo de 3** (3, 6 o 9):
$F(A,B,C,D) = \Sigma m(3, 6, 9) + d(10, 11, 12, 13, 14, 15)$. Obtenga la SOP mínima y compare el número de literales con el de la solución sin usar las X.

---

## Bloque E. Implementación con NAND y NOR

**Ejercicio 3.10 (Piensa, pareja, comparte).**

a) En el circuito NAND-NAND de $F = A + BD + BC$, ¿por qué $A$ entra complementada y $B$, $C$ y $D$ no?
b) Convierta $F = \overline{A}\,\overline{C} + BC$ (resultado del ejercicio 3.2) a NAND-NAND. ¿Cuántos chips 7400 necesita?

**Ejercicio 3.11.** Convierta $F = \overline{B}\,\overline{D} + BD$ (ejercicio 3.4) a NAND-NAND y calcule cuántos chips 7400 requiere. Compare con implementarla directamente con una compuerta XNOR.

**Ejercicio 3.12.** Convierta $F = (A + B)(\overline{A} + C)$ a NOR-NOR. ¿Cuántos chips 7402 se necesitan?

---

## Bloque F. Proyecto integrador

**Ejercicio 3.13.** Un equipo propone un sistema que requiere 24 entradas manuales y 6 dígitos de visualización. Explique por qué no cabe en la Basys 3 y proponga una modificación que respete los recursos de la tarjeta (16 interruptores, 5 pulsadores, 16 LED y 4 dígitos de 7 segmentos).

---

[← Anterior: Resumen](./resumen.md) | [Siguiente: Soluciones →](./soluciones.md)
