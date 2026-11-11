# Semana 2: Ejercicios

**Tema:** Álgebra de Boole y formas canónicas

> **Indicaciones:** En los problemas de diseño entregue: (1) tabla de verdad, (2) $\Sigma m$ y $\Pi M$, (3) SOP canónica, (4) versión simplificada y (5) recuento de compuertas y circuitos integrados. Ordene las variables alfabéticamente o según se indique, con la primera como bit más significativo.

---

## Bloque A. Leyes de De Morgan

**Ejercicio 2.1.** Aplique las leyes de De Morgan y simplifique la expresión resultante cuando sea posible:

a) $\overline{A\cdot B\cdot C}$
b) $\overline{A + \overline{B}\,C}$
c) $\overline{\overline{A}\,B + C}$
d) $\overline{\overline{A} + BC}$

> **Pista:** verifique cada respuesta evaluando una fila de la tabla de verdad.

---

## Bloque B. Minitérminos y maxitérminos

**Ejercicio 2.2.** Para tres variables $A, B, C$:

a) Escriba $m_4$ y $M_4$. Compruebe que $M_4 = \overline{m_4}$.
b) Escriba $m_5$ y $M_2$.
c) Una función tiene $F = \Sigma m(1, 2, 4, 7)$. Exprésela como $\Pi M$.

---

## Bloque C. Teoremas y simplificación algebraica

**Ejercicio 2.3.** Demuestre algebraicamente indicando el teorema empleado en cada paso:

a) $A + \overline{A}B = A + B$
b) $AB + A\overline{B} + \overline{A}B = A + B$
c) $(A + B)(A + C) = A + BC$

**Ejercicio 2.4.** Simplifique al mínimo:

a) $F = A + \overline{A}B + A\overline{B}C$ (ejemplo de la teoría; verifique el resultado con la fila $A=0, B=0, C=1$).
b) $F = AB + \overline{A}C + BC$
c) $F = \overline{A}BC + A\overline{B}C + ABC + AB\overline{C}$

---

## Bloque D. Interpretación del enunciado

**Ejercicio 2.5.** Un portón se abre cuando se cumple *«el control está presionado y el sensor de obstáculo está libre, o bien la llave maestra está girada»*. Defina variables, construya la tabla de verdad, escriba $\Sigma m$ y $\Pi M$, y simplifique.

**Ejercicio 2.6.** Una función de tres variables tiene $F = 1$ solo en las filas 0 y 7. Escriba su SOP canónica, su POS canónica y decida, justificando, qué forma conviene si únicamente se dispone de compuertas NOR.

---

## Bloque E. Taller de diseño por grupos

Para cada problema entregue: tabla de verdad · $\Sigma m$ y $\Pi M$ · SOP canónica · versión simplificada · recuento de compuertas y CI.

**Problema 2.7 (Luz de pasillo).** Dos interruptores $A$ y $B$ conmutan la luz; el interruptor maestro $M$ ($M = 1$) la apaga siempre. Orden de variables: $A, B, M$.

**Problema 2.8 (Detector de primos).** Entrada de 3 bits $ABC$ ($0$ a $7$). $F = 1$ si el número es primo.

**Problema 2.9 (Bomba de agua).** La bomba se enciende si hay agua en la cisterna ($B$) **y** el tanque está bajo ($A$) **o** se pide en manual ($C$). Orden: $A, B, C$.

**Problema 2.10 (Aviso de cinturón).** La alarma suena si el motor está encendido ($E$) **y** el cinturón no está puesto **o** la puerta está abierta ($P$). Defina $C = 1$ cuando el cinturón **está puesto**. Orden: $E, C, P$.

> **Nota:** En los problemas 2.9 y 2.10 declare explícitamente cómo interpretó la precedencia de «y» / «o» en el enunciado.

---

## Ticket de salida

1. Aplique De Morgan: $\overline{\overline{A} + BC}$.
2. Escriba $m_4$ y $M_4$.

---

[← Anterior: Resumen](./resumen.md) | [Siguiente: Soluciones →](./soluciones.md)
