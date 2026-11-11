# Semana 3: Soluciones

---

## Bloque A. Mapas de Karnaugh en SOP

### Ejercicio 3.1 (T1)

$F(A,B,C) = \Sigma m(1, 3, 4, 6)$:

| $A \backslash BC$ | 00 | 01 | 11 | 10 |
|:-----------------:|:--:|:--:|:--:|:--:|
| **0**             | 0  | 1  | 1  | 0  |
| **1**             | 1  | 0  | 0  | 1  |

| Grupo | Celdas | Variables constantes | Término |
|:-----:|:------:|----------------------|:-------:|
| 1 | $m_1, m_3$ | $A = 0$, $C = 1$ ($B$ cambia) | $\overline{A}C$ |
| 2 | $m_4, m_6$ (columnas 00 y 10, enrolladas) | $A = 1$, $C = 0$ ($B$ cambia) | $A\overline{C}$ |

$$
F = \overline{A}C + A\overline{C} = A \oplus C
$$

Es la compuerta **XOR** entre $A$ y $C$. Los 1 forman un patrón alternado: no existen grupos mayores.

### Ejercicio 3.2 (T2)

$F(A,B,C,D) = \Sigma m(0, 1, 4, 5, 6, 7, 14, 15)$:

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 1  | 0  | 0  |
| **01**             | 1  | 1  | 1  | 1  |
| **11**             | 0  | 0  | 1  | 1  |
| **10**             | 0  | 0  | 0  | 0  |

**Implicantes primos:**

| Primo | Celdas | Término |
|:-----:|:------:|:-------:|
| $P_1$ | $m_0, m_1, m_4, m_5$ | $\overline{A}\,\overline{C}$ |
| $P_2$ | $m_4, m_5, m_6, m_7$ | $\overline{A}B$ |
| $P_3$ | $m_6, m_7, m_{14}, m_{15}$ | $BC$ |

**Esenciales:** $m_0$ solo lo cubre $P_1$ $\Rightarrow$ $P_1$ es esencial; $m_{14}$ solo lo cubre $P_3$ $\Rightarrow$ $P_3$ es esencial. Entre ambos cubren $m_0, m_1, m_4, m_5, m_6, m_7, m_{14}, m_{15}$, es decir, **todos** los 1. El primo $P_2$ resulta **redundante**.

$$
\boxed{F = \overline{A}\,\overline{C} + BC}
$$

*Verificación:* $\overline{A}\,\overline{C}$ cubre $\{0,1,4,5\}$ y $BC$ cubre $\{6,7,14,15\}$: unión $= \{0,1,4,5,6,7,14,15\}$ ✓.

### Ejercicio 3.3 (T3)

$F(A,B,C,D) = \Sigma m(0, 2, 5, 8, 10, 13)$:

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 0  | 0  | 1  |
| **01**             | 0  | 1  | 0  | 0  |
| **11**             | 0  | 1  | 0  | 0  |
| **10**             | 1  | 0  | 0  | 1  |

- Las cuatro esquinas $\{m_0, m_2, m_8, m_{10}\}$: $B = 0$, $D = 0$ $\Rightarrow \overline{B}\,\overline{D}$.
- Par $\{m_5, m_{13}\}$ (filas 01 y 11): $B = 1$, $C = 0$, $D = 1$; $A$ cambia $\Rightarrow B\overline{C}D$.

$$
\boxed{F = \overline{B}\,\overline{D} + B\overline{C}D}
$$

Ambos grupos son esenciales ($m_0$ solo en el primero; $m_5$ solo en el segundo).

### Ejercicio 3.4 (Ticket de salida)

$F = \Sigma m(0, 2, 5, 7, 8, 10, 13, 15)$ (mapa en la sección 11 del resumen):

- Esquinas: $\overline{B}\,\overline{D}$. Bloque central $\{m_5, m_7, m_{13}, m_{15}\}$: $BD$.

$$
\boxed{F = \overline{B}\,\overline{D} + BD = \overline{B \oplus D}}
$$

Es una compuerta **XNOR** entre $B$ y $D$.

---

## Bloque B. Diagnóstico de errores

### Ejercicio 3.5 (T4)

La función correcta es la del ejercicio 3.2, con $F = \overline{A}\,\overline{C} + BC$.

| N.º | Error | Explicación |
|:---:|-------|-------------|
| 1 | **Orden de columnas incorrecto** | El mapa rotula las columnas como $00, 01, 10, 11$ (binario natural). Debe ser $00, 01, 11, 10$ (Gray); de lo contrario, celdas contiguas pueden diferir en dos bits y los grupos pierden validez. |
| 2 | **$\overline{A}\,\overline{B}\,\overline{C}$ no es primo** | Cubre $m_0, m_1$, que ya forman parte del grupo mayor $\overline{A}\,\overline{C}$ $\{m_0, m_1, m_4, m_5\}$. El grupo no se agrandó al máximo; el término sobra. |
| 3 | **$\overline{A}B$ es redundante** | Aunque es un implicante primo, sus celdas $\{m_4, m_5, m_6, m_7\}$ ya están cubiertas por $\overline{A}\,\overline{C}$ ($m_4, m_5$) y $BC$ ($m_6, m_7$); no es esencial y no aporta ningún 1 nuevo. |

> **Nota:** los términos $\overline{A}\,\overline{C}$ y $BC$ del estudiante son correctos; el error consiste en añadir términos innecesarios.

$$
\boxed{F = \overline{A}\,\overline{C} + BC}
$$

---

## Bloque C. Mapas en POS

### Ejercicio 3.6

Ceros de $F = \Sigma m(1,3,4,6)$: filas $0, 2, 5, 7$.

| $A \backslash BC$ | 00 | 01 | 11 | 10 |
|:-----------------:|:--:|:--:|:--:|:--:|
| **0**             | 0  | 1  | 1  | 0  |
| **1**             | 1  | 0  | 0  | 1  |

| Grupo de ceros | Celdas | Constantes | Suma (lectura invertida) |
|:--------------:|:------:|------------|:------------------------:|
| 1 | $m_0, m_2$ (enrolladas) | $A = 0$, $C = 0$ | $(A + C)$ |
| 2 | $m_5, m_7$ | $A = 1$, $C = 1$ | $(\overline{A} + \overline{C})$ |

$$
F = (A + C)(\overline{A} + \overline{C})
$$

| Forma | Expresión | Literales |
|:-----:|-----------|:---------:|
| SOP | $\overline{A}C + A\overline{C}$ | 4 |
| POS | $(A + C)(\overline{A} + \overline{C})$ | 4 |

Ambas tienen el mismo costo y representan la misma función, $A \oplus C$.

### Ejercicio 3.7

Celdas con 0 de $F = \Sigma m(0,1,2,5,8,9,10)$: $\{3, 4, 6, 7, 11, 12, 13, 14, 15\}$.

| Suma | Vale 0 cuando | Celdas con 0 que cubre |
|:----:|---------------|:----------------------:|
| $(\overline{A} + \overline{B})$ | $A = 1$ y $B = 1$ | $12, 13, 14, 15$ |
| $(\overline{B} + D)$ | $B = 1$ y $D = 0$ | $4, 6, 12, 14$ |
| $(\overline{C} + \overline{D})$ | $C = 1$ y $D = 1$ | $3, 7, 11, 15$ |

Unión: $\{3, 4, 6, 7, 11, 12, 13, 14, 15\}$, que coincide con el conjunto de ceros de $F$, y ninguna suma vale 0 en una celda con $F = 1$ ✓. La POS tiene 6 literales frente a los 7 de la SOP.

---

## Bloque D. Condiciones indiferentes

### Ejercicio 3.8 (BCD par)

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 1  | 0  | 0  | 1  |
| **01**             | 1  | 0  | 0  | 1  |
| **11**             | X  | X  | X  | X  |
| **10**             | 1  | 0  | X  | X  |

Las columnas $CD = 00$ y $CD = 10$ son vecinas (el mapa se enrolla). Aprovechando las X se forma un único grupo de **8 celdas** ($m_0, m_2, m_4, m_6, m_8, m_{10}, m_{12}, m_{14}$), con $D = 0$ constante y $A$, $B$, $C$ variables:

$$
\boxed{F = \overline{D}}
$$

Es coherente con el sentido de la función: un dígito es par si y solo si su bit menos significativo vale 0. Sin usar las X se necesitarían varios términos.

### Ejercicio 3.9 (BCD múltiplo de 3)

| $AB \backslash CD$ | 00 | 01 | 11 | 10 |
|:------------------:|:--:|:--:|:--:|:--:|
| **00**             | 0  | 0  | 1  | 0  |
| **01**             | 0  | 0  | 0  | 1  |
| **11**             | X  | X  | X  | X  |
| **10**             | 0  | 1  | X  | X  |

| Grupo | Celdas | Uso de X | Término |
|:-----:|:------:|----------|:-------:|
| 1 | $m_9, m_{11}, m_{13}, m_{15}$ | $m_{11}, m_{13}, m_{15}$ como 1 | $AD$ |
| 2 | $m_6, m_{14}$ | $m_{14}$ como 1 | $BC\overline{D}$ |
| 3 | $m_3, m_{11}$ | $m_{11}$ como 1 | $\overline{B}CD$ |

$$
\boxed{F = AD + BC\overline{D} + \overline{B}CD} \qquad (8 \text{ literales})
$$

*Sin usar las X*, los tres 1 ($m_3, m_6, m_9$) están aislados (no tienen vecinos con 1), de modo que se necesitarían tres minitérminos de 4 literales: **12 literales**. Las condiciones indiferentes ahorran 4 literales.

*Verificación:* $m_3 = 0011$ $\Rightarrow \overline{B}CD = 1$ ✓; $m_6 = 0110$ $\Rightarrow BC\overline{D} = 1$ ✓; $m_9 = 1001$ $\Rightarrow AD = 1$ ✓; y $m_0, m_1, m_2, m_4, m_5, m_7, m_8$ dan 0 ✓.

---

## Bloque E. Implementación con NAND y NOR

### Ejercicio 3.10

**a)** En $F = A + BD + BC$, el literal $A$ está solo en su término: no existe compuerta de primer nivel que lo procese. La NAND de salida calcula $\overline{X\cdot Y\cdot Z}$; para que entregue $A + \ldots$ la entrada correspondiente debe ser $\overline{A}$, pues por De Morgan $\overline{\overline{A}\cdot\overline{BD}\cdot\overline{BC}} = A + BD + BC$. En cambio, $BD$ y $BC$ ya pasan por una NAND de primer nivel, que entrega $\overline{BD}$ y $\overline{BC}$, es decir, ya están complementados.

**b)** $F = \overline{A}\,\overline{C} + BC$:

$$
F = \overline{\overline{\overline{A}\,\overline{C}}\cdot\overline{BC}} = \text{NAND}\big(\text{NAND}(\overline{A},\overline{C}),\ \text{NAND}(B,C)\big)
$$

| Compuerta | Función |
|:---------:|---------|
| $G_1$ | $\overline{A} = \text{NAND}(A,A)$ |
| $G_2$ | $\overline{C} = \text{NAND}(C,C)$ |
| $G_3$ | $\text{NAND}(\overline{A},\overline{C})$ |
| $G_4$ | $\text{NAND}(B,C)$ |
| $G_5$ | NAND de salida |

Se requieren **5 NAND de 2 entradas**. Un 7400 contiene 4, por lo tanto se necesitan **2 chips 7400**.

### Ejercicio 3.11

$F = \overline{B}\,\overline{D} + BD$:

| Compuerta | Función |
|:---------:|---------|
| $G_1$ | $\overline{B} = \text{NAND}(B,B)$ |
| $G_2$ | $\overline{D} = \text{NAND}(D,D)$ |
| $G_3$ | $\text{NAND}(\overline{B},\overline{D})$ |
| $G_4$ | $\text{NAND}(B,D)$ |
| $G_5$ | NAND de salida |

Son **5 NAND**, es decir, **2 chips 7400**. Con una compuerta **XNOR** directa bastan **1 compuerta y 1 CI** (o una XOR más un inversor). Esto ilustra que la conversión a NAND es útil para uniformar la familia de compuertas, pero el reconocimiento de la función ($F = \overline{B \oplus D}$) puede ahorrar más.

### Ejercicio 3.12

$$
F = (A + B)(\overline{A} + C) = \overline{\overline{(A+B)} + \overline{(\overline{A}+C)}} = \text{NOR}\big(\text{NOR}(A,B),\ \text{NOR}(\overline{A},C)\big)
$$

| Compuerta | Función |
|:---------:|---------|
| $G_1$ | $\overline{A} = \text{NOR}(A,A)$ |
| $G_2$ | $\text{NOR}(A,B)$ |
| $G_3$ | $\text{NOR}(\overline{A},C)$ |
| $G_4$ | NOR de salida |

Son **4 NOR de 2 entradas**: exactamente un chip **7402**.

---

## Bloque F. Proyecto integrador

### Ejercicio 3.13

| Recurso | Requerido | Disponible en la Basys 3 | ¿Cabe? |
|---------|:---------:|:------------------------:|:------:|
| Entradas manuales | 24 | 16 interruptores + 5 pulsadores = 21 | No |
| Dígitos de 7 segmentos | 6 | 4 | No |

**Modificación propuesta:** reducir las entradas a un máximo de 21 (por ejemplo, agrupar condiciones o codificar en menos bits) y mostrar la información en 4 dígitos como máximo, o repartirla entre los 4 dígitos y los 16 LED. El sistema debe diseñarse desde la especificación respetando estos recursos.

---

[← Anterior: Ejercicios](./ejercicios.md) | [Siguiente semana: Circuitos aritméticos →](../semana-04/resumen.md)
