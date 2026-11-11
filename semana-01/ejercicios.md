# Semana 1: Ejercicios

**Tema:** Sistemas numéricos, códigos y compuertas lógicas

> **Indicaciones:** Resuelva cada ejercicio mostrando el procedimiento. Verifique siempre el resultado con un método alterno (por ejemplo, reconvirtiendo a decimal mediante los pesos).

---

## Bloque A. Sistemas numéricos

**Ejercicio 1.1 (Reto de conversión).**

a) Convierta $45_{10}$ a binario y a hexadecimal.
b) Convierta $\mathrm{A7}_{16}$ a decimal.
c) Convierta $11100101_2$ a hexadecimal y a octal.

**Ejercicio 1.2.** Convierta $200_{10}$ a binario mediante divisiones sucesivas entre 2, y luego exprese el resultado en hexadecimal y en octal.

**Ejercicio 1.3.** Determine el valor decimal de $10110110_2$ empleando los pesos de cada posición. Exprese además el número en hexadecimal.

**Ejercicio 1.4.** Realice la suma binaria $1101_2 + 0111_2$ indicando el acarreo de cada columna. Verifique en decimal.

---

## Bloque B. Niveles lógicos y margen de ruido

Considere la familia 74LS con $V_{OH(\min)} = 2{,}7\ \text{V}$, $V_{IH(\min)} = 2{,}0\ \text{V}$, $V_{IL(\max)} = 0{,}8\ \text{V}$ y $V_{OL(\max)} = 0{,}5\ \text{V}$.

**Ejercicio 1.5.**

a) Calcule los márgenes de ruido alto y bajo.
b) Una salida entrega un 0 de 0,5 V y se induce un ruido de 0,25 V. ¿Qué lee la compuerta receptora?
c) Una salida entrega un 1 de 2,7 V y la línea pierde 0,8 V por caída en el trayecto. ¿Se interpreta correctamente como 1? Justifique.

---

## Bloque C. Complemento a dos

**Ejercicio 1.6.**

a) Represente $-6$ y $-1$ en complemento a dos con 4 bits.
b) Represente $-25$ en complemento a dos con 8 bits.
c) Determine el valor decimal de $1101_2$ (4 bits) y de $10010110_2$ (8 bits), ambos en complemento a dos.

**Ejercicio 1.7.** Con 4 bits en complemento a dos, efectúe las siguientes operaciones sumando el negativo del sustraendo y determine si hay desbordamiento:

a) $7 - 5$
b) $3 - 5$
c) $(-5) + (-4)$

> **Pista:** Hay desbordamiento cuando el resultado exacto está fuera del rango $[-8, +7]$.

---

## Bloque D. Códigos

**Ejercicio 1.8.**

a) Escriba $359_{10}$ en BCD.
b) Indique si $1100\,0101_{\text{BCD}}$ es una representación válida. Justifique.
c) Construya el código Gray de 4 bits para las posiciones 7 y 8 con el método del espejo, y compare cuántos bits cambian entre ambas posiciones en binario natural y en Gray.

**Ejercicio 1.9.**

a) Codifique la palabra «UNL» en ASCII (decimal y hexadecimal). Dato: $A = 65$.
b) Decodifique la secuencia `0x43 0x4F 0x44 0x45`.

---

## Bloque E. Compuertas lógicas

**Ejercicio 1.10 (Del enunciado a la compuerta).** Indique la compuerta que describe cada enunciado:

a) La alarma suena solo si las dos puertas están abiertas.
b) La luz del pasillo se enciende si se pulsa cualquiera de los dos botones.
c) El juego marca «diferentes» si los dos jugadores eligen distinto.
d) La bomba de agua se apaga cuando el sensor de nivel está activo.

**Ejercicio 1.11 (Tabla de verdad).**

a) Elabore la tabla de verdad de $Y = A\cdot B + \overline{C}$. Incluya las columnas intermedias $A\cdot B$ y $\overline{C}$ y una columna con el valor decimal de $ABC$.
b) Elabore la tabla de verdad de $Y = (A + B)\cdot\overline{C}$ y exprese la función como lista de minitérminos (filas con $Y = 1$).

**Ejercicio 1.12 (Circuito integrado).**

a) Para el 74LS08, indique los pines de alimentación y de tierra, y los pines de entrada y salida de la compuerta 3.
b) Interprete el código impreso `SN74LS08N`.
c) Explique qué ocurre si una entrada del chip queda sin conectar.
d) El proveedor solo dispone de 74HC08. ¿Puede utilizarlo? Justifique.

---

[← Anterior: Resumen](./resumen.md) | [Siguiente: Soluciones →](./soluciones.md)
