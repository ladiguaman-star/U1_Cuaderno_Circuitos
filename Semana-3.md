# Semana 3: Mapas de Karnaugh, condiciones indiferentes y universalidad NAND/NOR

**Unidad 1 · Análisis de lógica combinacional con diseño clásico**
**Resultado de aprendizaje R1:** diseña e implementa circuitos combinacionales básicos utilizando técnicas de diseño clásico.

> **Nota:** Este capítulo integra las dos sesiones de la semana: la Sesión 1 (mapas de Karnaugh en SOP y POS) y la Sesión 2 (condiciones indiferentes, implementación con una sola familia de compuertas y lanzamiento del proyecto integrador).

## Objetivos de la semana

Al finalizar el estudio de este capítulo, el lector podrá:

- Obtener la expresión mínima en SOP y en POS de funciones de 3 y 4 variables mediante mapas de Karnaugh, justificando cada agrupación.
- Minimizar funciones con condiciones indiferentes.
- Implementar una función con una sola familia de compuertas (NAND o NOR), cuantificando el ahorro en compuertas y circuitos integrados.

---

## 1. El problema del mínimo

Considérese la función $F(A,B,C) = \Sigma m(0, 2, 4, 5, 6)$:

| $A$ | $B$ | $C$ | $F$   |
|:---:|:---:|:---:|:-----:|
| 0   | 0   | 0   | **1** |
| 0   | 0   | 1   | 0     |
| 0   | 1   | 0   | **1** |
| 0   | 1   | 1   | 0     |
| 1   | 0   | 0   | **1** |
| 1   | 0   | 1   | **1** |
| 1   | 1   | 0   | **1** |
| 1   | 1   | 1   | 0     |

El álgebra de Boole de la Semana 2 permite simplificar, pero **no garantiza que el resultado sea el mínimo**. El mapa de Karnaugh convierte la búsqueda de términos adyacentes en un problema visual.

---

## 2. Fundamento: el teorema de adyacencia

$$
XY + X\overline{Y} = X
$$

Si dos minitérminos difieren en una sola variable, esa variable desaparece:

$$
m_4 + m_5 = A\overline{B}\,\overline{C} + A\overline{B}C = A\overline{B}
$$

| Minitérmino | $A\,B\,C$ |
|:-----------:|:---------:|
| $m_4$       | 1 0 0     |
| $m_5$       | 1 0 1     |
| Resultado   | 1 0 $-$ $\Rightarrow A\overline{B}$ |

### 2.1 ¿Por qué el orden 00, 01, 11, 10?

Para que celdas contiguas del mapa difieran en un solo bit se emplea el **código Gray** en los encabezados:

| Binario | Cambio entre vecinos | Gray | Cambio entre vecinos |
|:-------:|:--------------------:|:----:|:--------------------:|
| 00      |                      | 00   |                      |
| 01      | 1 bit                | 01   | 1 bit                |
| 10      | 2 bits               | 11   | 1 bit                |
| 11      | 1 bit                | 10   | 1 bit                |
| (00)    | 2 bits               | (00) | 1 bit                |

En Gray, cada celda es vecina lógica de la siguiente **y la última lo es de la primera**.

![Comparación del orden binario y del orden Gray en los encabezados de un mapa de Karnaugh](./assets/orden-gray-karnaugh.png)

*Figura 3.1: Orden binario (cambian 2 bits en algunas transiciones) frente al orden Gray (cambia un bit siempre).*

---

## 3. Mapa de Karnaugh de 3 variables

- **Filas:** variable $A$.
- **Columnas:** $BC$ en código Gray ($00, 01, 11, 10$).
- **Cada celda** corresponde a un minitérmino: 8 celdas = 8 filas de la tabla de verdad.

| $A \backslash BC$ | 00 | 01 | 11 | 10 |
|:-----------------:|:--:|:--:|:--:|:--:|
| **0**             | $m_0$ | $m_1$ | $m_3$ | $m_2$ |
| **1**             | $m_4$ | $m_5$ | $m_7$ | $m_6$ |

> **Atención:** $m_3$ aparece antes que $m_2$.

![Mapa de Karnaugh de 3 variables con la numeración de minitérminos](./assets/mapa-karnaugh-3-variables.png)

*Figura 3.2: Mapa de Karnaugh de 3 variables con la numeración de sus minitérminos.*

---

## 4. Reglas para agrupar

| Regla | Descripción |
|-------|-------------|
| **Tamaño $2^k$** | Los grupos contienen 1, 2, 4, 8 o 16 celdas; un grupo de $2^k$ celdas elimina $k$ variables |
| **Rectangulares** | No se admiten formas en L ni diagonales |
| **Lo más grande posible** | Los grupos grandes producen términos más cortos |
| **El mapa se enrolla** | Los bordes opuestos y las esquinas son vecinos |

Para una función de $n$ variables, un grupo de $2^k$ celdas genera un término con $n - k$ literales.

**Agrupaciones válidas e inválidas (3 variables):**

| Válido: grupo $C'$ (bordes enrollados) |     |     |     |     |
|:--------------------:|:--:|:--:|:--:|:--:|
| $A \backslash BC$    | 00 | 01 | 11 | 10 |
| 0                    | 1  | 0  | 0  | 1  |
| 1                    | 1  | 0  | 0  | 1  |

Las cuatro celdas $m_0, m_2, m_4, m_6$ forman un solo grupo (columnas 00 y 10 son vecinas): $F = \overline{C}$.

| No válido: grupo de 3 en forma de L |     |     |     |     |
|:--------------------:|:--:|:--:|:--:|:--:|
| $A \backslash BC$    | 00 | 01 | 11 | 10 |
| 0                    | 0  | 1  | 1  | 0  |
| 1                    | 0  | 0  | 1  | 0  |

Los tres 1 no forman un rectángulo de $2^k$ celdas: se agrupan como dos pares, $\{m_1, m_3\}$ y $\{m_3, m_7\}$.

![Ejemplos de agrupaciones válidas e inválidas en mapas de Karnaugh](./assets/reglas-agrupacion-karnaugh.png)

*Figura 3.3: Agrupaciones válidas (tamaño $2^k$, rectangulares, con bordes enrollados) y no válidas (grupo de 3 en L).*

### 4.1 Lectura de un grupo

Se conservan únicamente las variables que **no cambian** dentro del grupo:

- Variable constante en **1** → aparece sin complemento ($A$).
- Variable constante en **0** → aparece complementada ($\overline{A}$).
- Variable que **cambia** → desaparece.

### 4.2 El reto inicial resuelto en el mapa

$F = \Sigma m(0, 2, 4, 5, 6)$:

| $A \backslash BC$ | 00 | 01 | 11 | 10 |
|:-----------------:|:--:|:--:|:--:|:--:|
| **0**             | 1  | 0  | 0  | 1  |
| **1**             | 1  | 1  | 0  | 1  |

- Grupo de 4 $\{m_0, m_2, m_4, m_6\}$: $A$ y $B$ cambian; $C = 0$ en todo el grupo $\Rightarrow \overline{C}$.
- Grupo de 2 $\{m_4, m_5\}$: $A = 1$, $B = 0$; $C$ cambia $\Rightarrow A\overline{B}$.

$$
\boxed{F = \overline{C} + A\overline{B}}
$$

![Mapa de Karnaugh de la función F = Σm(0,2,4,5,6) con los grupos C' y AB' señalados](./assets/mapa-reto-inicial.png)

*Figura 3.4: Simplificación de $F = \Sigma m(0,2,4,5,6)$ en el mapa de 3 variables.*

---

## 5. Mapa de Karnaugh de 4 variables

- **Filas:** $AB$; **columnas:** $CD$, ambas en código Gray.

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | $m_0$ | $m_1$ | $m_3$ | $m_2$ |
| **01**             | $m_4$ | $m_5$ | $m_7$ | $m_6$ |
| **11**             | $m_{12}$ | $m_{13}$ | $m_{15}$ | $m_{14}$ |
| **10**             | $m_8$ | $m_9$ | $m_{11}$ | $m_{10}$ |

![Mapa de Karnaugh de 4 variables con la numeración de minitérminos](./assets/mapa-karnaugh-4-variables.png)

*Figura 3.5: Mapa de Karnaugh de 4 variables con la numeración de sus minitérminos.*

### 5.1 Bordes y esquinas también son vecinos

Puede imaginarse el mapa enrollado como un **toroide**: el borde superior toca al inferior y el izquierdo al derecho.

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 0  | 0  | 1  |
| **01**             | 0  | 0  | 0  | 0  |
| **11**             | 0  | 0  | 0  | 0  |
| **10**             | 1  | 0  | 0  | 1  |

Las **cuatro esquinas** ($m_0, m_2, m_8, m_{10}$) forman un grupo: $B = 0$ y $D = 0$ en todas, por lo que el término es $\overline{B}\,\overline{D}$.

![Mapa de 4 variables con las cuatro esquinas agrupadas en el término B'D'](./assets/mapa-esquinas-4-variables.png)

*Figura 3.6: Las cuatro esquinas del mapa forman un grupo válido (término $\overline{B}\,\overline{D}$).*

---

## 6. Implicantes primos y esenciales

| Concepto | Definición |
|----------|------------|
| **Implicante** | Cualquier grupo válido de 1 (o X): término producto que solo vale 1 donde $F$ vale 1 |
| **Implicante primo** | Grupo que ya no puede agrandarse más |
| **Primo esencial** | Único primo que cubre algún 1; debe estar en la solución |

> **Solución mínima = primos esenciales + los primos mínimos necesarios para cubrir los 1 restantes.**

---

## 7. Procedimiento para la SOP mínima

1. **Colocar** los 1, 0 y X en sus celdas.
2. **Agrupar** los 1 en los grupos más grandes posibles.
3. **Elegir** los primos esenciales.
4. **Cubrir** los 1 restantes con el menor número de grupos.
5. **Leer** un término por grupo y unirlos con OR.

### 7.1 Ejemplo guiado: $F = \Sigma m(0,1,2,5,8,9,10)$

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 1  | 0  | 1  |
| **01**             | 0  | 1  | 0  | 0  |
| **11**             | 0  | 0  | 0  | 0  |
| **10**             | 1  | 1  | 0  | 1  |

| Grupo | Celdas | Observación | Término |
|:-----:|:------:|-------------|:-------:|
| 1 | $m_0, m_1, m_8, m_9$ | Bordes superior e inferior | $\overline{B}\,\overline{C}$ |
| 2 | $m_0, m_2, m_8, m_{10}$ | Las 4 esquinas | $\overline{B}\,\overline{D}$ |
| 3 | $m_1, m_5$ | $B$ cambia; $A=0,\ C=0,\ D=1$ | $\overline{A}\,\overline{C}D$ |

$$
\boxed{F = \overline{B}\,\overline{C} + \overline{B}\,\overline{D} + \overline{A}\,\overline{C}D} \qquad (3 \text{ términos, } 7 \text{ literales})
$$

Los tres grupos son esenciales: $m_9$ solo está en el grupo 1, $m_2$ y $m_{10}$ solo en el grupo 2, y $m_5$ solo en el grupo 3.

![Mapa de Karnaugh de 4 variables con los tres grupos del ejemplo guiado](./assets/mapa-ejemplo-guiado-sop.png)

*Figura 3.7: Agrupación de $F = \Sigma m(0,1,2,5,8,9,10)$ en SOP mínima.*

---

## 8. La misma función en POS: se agrupan los 0

Para obtener la POS mínima se agrupan los **0** del mapa y se lee con **lectura invertida**: variable constante en 0 → $A$ (sin complemento); constante en 1 → $\overline{A}$.

| Grupo de ceros | Celdas | Observación | Suma |
|:--------------:|:------:|-------------|:----:|
| Fila $AB = 11$ | $m_{12}, m_{13}, m_{14}, m_{15}$ | $A = 1, B = 1$ | $(\overline{A} + \overline{B})$ |
| Columna $CD = 11$ | $m_3, m_7, m_{11}, m_{15}$ | $C = 1, D = 1$ | $(\overline{C} + \overline{D})$ |
| Bordes izquierdo y derecho, filas 01 y 11 | $m_4, m_6, m_{12}, m_{14}$ | $B = 1, D = 0$ | $(\overline{B} + D)$ |

$$
\boxed{F = (\overline{A} + \overline{B})(\overline{B} + D)(\overline{C} + \overline{D})}
$$

![Mapa de Karnaugh con los grupos de ceros para la obtención de la POS mínima](./assets/mapa-ejemplo-guiado-pos.png)

*Figura 3.8: Agrupación de los 0 de $F = \Sigma m(0,1,2,5,8,9,10)$ para obtener la POS mínima.*

### 8.1 ¿SOP o POS? Se cuentan los literales

| Forma | Expresión | Literales |
|:-----:|-----------|:---------:|
| SOP   | $\overline{B}\,\overline{C} + \overline{B}\,\overline{D} + \overline{A}\,\overline{C}D$ | 7 |
| POS   | $(\overline{A}+\overline{B})(\overline{B}+D)(\overline{C}+\overline{D})$ | 6 |

> **Criterio:** construir ambas formas y elegir la de menor costo en literales, compuertas y circuitos integrados.

---

## 9. Condiciones indiferentes (don't care)

Un dígito BCD usa 4 bits, pero solo 10 de las 16 combinaciones. Las combinaciones $1010$ a $1111$ **nunca ocurren**; ¿qué debe hacer el circuito con ellas? **Lo que más convenga.**

Notación: $F = \Sigma m(\ldots) + d(\ldots)$.

| Uso de la X | Descripción |
|:-----------:|-------------|
| **Como 1**  | Si agranda un grupo, se incluye: el término queda más corto |
| **Como 0**  | Si no ayuda, se ignora; ninguna X está obligada a quedar cubierta |
| **Nunca sola** | Un grupo formado solo por X agrega un término inútil |

### 9.1 Ejemplo guiado: dígito BCD $\geq 5$

$$
F = \Sigma m(5, 6, 7, 8, 9) + d(10, 11, 12, 13, 14, 15)
$$

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 0  | 0  | 0  | 0  |
| **01**             | 0  | 1  | 1  | 1  |
| **11**             | X  | X  | X  | X  |
| **10**             | 1  | 1  | X  | X  |

| Caso | Expresión | Literales |
|------|-----------|:---------:|
| Sin usar las X | $A\overline{B}\,\overline{C} + \overline{A}BD + \overline{A}BC$ | 9 |
| Con las X      | $F = A + BD + BC$ | **5** |

*Lectura con las X:* $A$ cubre la fila 11 y la fila 10 completas ($m_8$ a $m_{15}$); $BD$ cubre $m_5, m_7, m_{13}, m_{15}$; $BC$ cubre $m_6, m_7, m_{14}, m_{15}$.

![Comparación de la minimización del dígito BCD mayor o igual a 5 con y sin condiciones indiferentes](./assets/mapa-bcd-mayor-igual-5.png)

*Figura 3.9: Mapa de $F = \Sigma m(5,6,7,8,9) + d(10,\ldots,15)$ sin usar las X (9 literales) y usándolas (5 literales).*

---

## 10. Universalidad de las compuertas NAND y NOR

### 10.1 Construcción con NAND

| Función | Construcción con NAND | Justificación |
|:-------:|:---------------------:|:-------------:|
| NOT | $\overline{A\cdot A} = \overline{A}$ | Entradas unidas |
| AND | $\overline{\overline{AB}}= AB$ | NAND seguida de NOT |
| OR  | $\overline{\overline{A}\cdot\overline{B}} = A + B$ | De Morgan con entradas negadas |

Como NOT, AND y OR se construyen con NAND, **cualquier función combinacional** también.

![Construcción de las compuertas NOT, AND y OR utilizando únicamente compuertas NAND](./assets/universalidad-nand.png)

*Figura 3.10: Realización de NOT, AND y OR con compuertas NAND.*

### 10.2 NOR: el caso dual

| Función | Solo NAND | Solo NOR |
|:-------:|:---------:|:--------:|
| NOT | $\overline{A\cdot A}$ | $\overline{A + A}$ |
| AND | $\overline{\overline{AB}}$ | $\overline{\overline{A} + \overline{B}}$ |
| OR  | $\overline{\overline{A}\cdot\overline{B}}$ | $\overline{\overline{A + B}}$ |

| Forma mínima | Implementación natural |
|:------------:|:----------------------:|
| SOP mínima   | **NAND-NAND**          |
| POS mínima   | **NOR-NOR**            |

> La forma mínima elegida decide la familia que conviene.

### 10.3 De SOP a NAND-NAND en cuatro pasos

Sea $F = A + BD + BC$ (SOP mínima del ejemplo BCD):

| Paso | Expresión | Justificación |
|:----:|-----------|---------------|
| 1 | $F = A + BD + BC$ | SOP mínima |
| 2 | $F = \overline{\overline{A + BD + BC}}$ | Doble negación (no cambia nada) |
| 3 | $F = \overline{\overline{A}\cdot\overline{BD}\cdot\overline{BC}}$ | De Morgan sobre la negación interna |
| 4 | $F = \text{NAND}\big(\overline{A},\ \text{NAND}(B,D),\ \text{NAND}(B,C)\big)$ | Cada paréntesis es una NAND |

![Circuito NAND-NAND de dos niveles que implementa F = A + BD + BC](./assets/circuito-nand-nand.png)

*Figura 3.11: Implementación NAND-NAND de $F = A + BD + BC$. El literal $A$ entra complementado (una NAND usada como inversor).*

**Observaciones:**

- **Dos niveles:** el retardo es el mismo que el de AND-OR.
- **Una familia:** toda la red se construye con los chips 7400 (NAND de 2 entradas) y 7410 (NAND de 3 entradas).
- **El literal solo se complementa:** $A$ no forma parte de ningún producto, por lo que no tiene compuerta de primer nivel; para que la NAND de salida lo convierta en $+A$ debe entrar como $\overline{A}$. Las variables $B$, $C$ y $D$ ya están dentro de productos, cuya NAND realiza la negación.

### 10.4 Conversión de POS a NOR-NOR

Análogamente, si $F = (A+B)(\overline{A}+C)$:

$$
F = \overline{\overline{(A+B)(\overline{A}+C)}} = \overline{\overline{(A+B)} + \overline{(\overline{A}+C)}} = \text{NOR}\big(\text{NOR}(A,B),\ \text{NOR}(\overline{A},C)\big)
$$

con $\overline{A} = \text{NOR}(A, A)$ como inversor. Se requieren 4 NOR de 2 entradas: un solo chip 7402.

### 10.5 ¿Cuántos circuitos integrados cuesta?

| Versión de $F = \Sigma m(5,\ldots,9) + d(10,\ldots,15)$ | Circuitos integrados | CI |
|---------------------------------------------------------|----------------------|:--:|
| Sin usar las X (AND-OR) | 7404 + 7411 + 7432 | **3** |
| Con X, AND-OR           | 7408 + 7432        | **2** |
| Con X, solo NAND        | 7400 + 7410        | **2** |

> **Conclusión:** el ahorro proviene de las X; la conversión a NAND no agrega chips y deja una sola familia en el inventario. Se compara siempre en literales **y** en chips: el mínimo algebraico no siempre es el más barato.

---

## 11. El ticket de la Sesión 1, resuelto

$F(A,B,C,D) = \Sigma m(0, 2, 5, 7, 8, 10, 13, 15)$:

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 0  | 0  | 1  |
| **01**             | 0  | 1  | 1  | 0  |
| **11**             | 0  | 1  | 1  | 0  |
| **10**             | 1  | 0  | 0  | 1  |

- Las 4 esquinas: $\overline{B}\,\overline{D}$.
- El bloque central ($m_5, m_7, m_{13}, m_{15}$): $BD$.

$$
\boxed{F = \overline{B}\,\overline{D} + BD = \overline{B \oplus D}}
$$

Es la compuerta **XNOR** de la Semana 1: vale 1 cuando $B$ y $D$ son iguales.

![Mapa de Karnaugh del ticket de salida: esquinas B'D' y bloque central BD](./assets/mapa-ticket-xnor.png)

*Figura 3.12: Simplificación de $F = \Sigma m(0,2,5,7,8,10,13,15)$, equivalente a una XNOR entre $B$ y $D$.*

---
