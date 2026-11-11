# Semana 1: Soluciones

---

## Bloque A. Sistemas numéricos

### Ejercicio 1.1

**a) $45_{10}$ a binario y hexadecimal.**

| División    | Cociente | Residuo |
|:-----------:|:--------:|:-------:|
| $45 \div 2$ | 22       | 1       |
| $22 \div 2$ | 11       | 0       |
| $11 \div 2$ | 5        | 1       |
| $5 \div 2$  | 2        | 1       |
| $2 \div 2$  | 1        | 0       |
| $1 \div 2$  | 0        | 1       |

Leyendo los residuos de abajo hacia arriba: $45_{10} = 101101_2$. Agrupando de 4 en 4 desde la derecha: $0010\,1101 = 2\mathrm{D}_{16}$.

*Verificación:* $32 + 8 + 4 + 1 = 45$ y $2\cdot 16 + 13 = 45$.

**b) $\mathrm{A7}_{16}$ a decimal.**

$$
\mathrm{A7}_{16} = 10 \cdot 16 + 7 \cdot 1 = 160 + 7 = 167_{10}
$$

**c) $11100101_2$ a hexadecimal y octal.**

- Hexadecimal: $1110\,0101 = \mathrm{E}\,5 \Rightarrow \mathrm{E5}_{16}$.
- Octal (se completa con un cero a la izquierda): $011\,100\,101 = 3\,4\,5 \Rightarrow 345_8$.

*Verificación:* $14\cdot16 + 5 = 229$ y $3\cdot 64 + 4\cdot 8 + 5 = 229$.

### Ejercicio 1.2

| División     | Cociente | Residuo |
|:------------:|:--------:|:-------:|
| $200 \div 2$ | 100      | 0       |
| $100 \div 2$ | 50       | 0       |
| $50 \div 2$  | 25       | 0       |
| $25 \div 2$  | 12       | 1       |
| $12 \div 2$  | 6        | 0       |
| $6 \div 2$   | 3        | 0       |
| $3 \div 2$   | 1        | 1       |
| $1 \div 2$   | 0        | 1       |

$$
200_{10} = 11001000_2 = \mathrm{C8}_{16} = 310_8
$$

*Verificación:* $128 + 64 + 8 = 200$; $12\cdot 16 + 8 = 200$; $3\cdot 64 + 1\cdot 8 = 200$.

### Ejercicio 1.3

Los bits en 1 están en las posiciones 7, 5, 4, 2 y 1:

$$
10110110_2 = 128 + 32 + 16 + 4 + 2 = 182_{10}
$$

En hexadecimal: $1011\,0110 = \mathrm{B6}_{16}$, y $11\cdot 16 + 6 = 182$.

### Ejercicio 1.4

```text
 acarreo   1 1 1 1
             1 1 0 1   (13)
           + 0 1 1 1   ( 7)
           ---------
           1 0 1 0 0   (20)
```

| Columna | Suma       | Escribo | Llevo |
|:-------:|:----------:|:-------:|:-----:|
| 0       | 1 + 1 = 2  | 0       | 1     |
| 1       | 0 + 1 + 1 = 2 | 0    | 1     |
| 2       | 1 + 1 + 1 = 3 | 1    | 1     |
| 3       | 1 + 0 + 1 = 2 | 0    | 1     |

Resultado: $10100_2 = 16 + 4 = 20_{10}$. Coincide con $13 + 7 = 20$.

---

## Bloque B. Niveles lógicos y margen de ruido

### Ejercicio 1.5

**a)**

$$
NM_H = 2{,}7 - 2{,}0 = 0{,}7\ \text{V} \qquad NM_L = 0{,}8 - 0{,}5 = 0{,}3\ \text{V}
$$

**b)** Voltaje en el receptor: $0{,}5 + 0{,}25 = 0{,}75\ \text{V}$. Como $0{,}75 \leq V_{IL(\max)} = 0{,}8\ \text{V}$ (y además $0{,}25 < NM_L = 0{,}3$), la compuerta lee **0** correctamente.

**c)** Voltaje en el receptor: $2{,}7 - 0{,}8 = 1{,}9\ \text{V}$. Como $1{,}9 < V_{IH(\min)} = 2{,}0\ \text{V}$, el valor cae en la zona indefinida (0,8 V a 2,0 V) y **no se garantiza** su lectura como 1. La pérdida de 0,8 V excede el margen $NM_H = 0{,}7\ \text{V}$.

---

## Bloque C. Complemento a dos

### Ejercicio 1.6

**a)**

- $-6$: $6 = 0110 \rightarrow$ invertir: $1001 \rightarrow +1$: $\mathbf{1010}$.
- $-1$: $1 = 0001 \rightarrow$ invertir: $1110 \rightarrow +1$: $\mathbf{1111}$.

**b)** $25 = 00011001 \rightarrow$ invertir: $11100110 \rightarrow +1$: $\mathbf{11100111}$.

*Verificación:* $-128 + 64 + 32 + 4 + 2 + 1 = -25$.

**c)**

$$
1101_2 = -8 + 4 + 0 + 1 = -3
$$

$$
10010110_2 = -128 + 16 + 4 + 2 = -106
$$

### Ejercicio 1.7

Se utiliza $A - B = A + (-B)$ con $-5 = 1011$ y $-4 = 1100$.

**a) $7 - 5$**

```text
   0111   (+7)
 + 1011   (−5)
 ------
 1 0010   -> se descarta el bit sobrante -> 0010 = +2
```

Resultado correcto, sin desbordamiento.

**b) $3 - 5$**

```text
   0011   (+3)
 + 1011   (−5)
 ------
   1110   -> −8 + 4 + 2 = −2
```

Resultado correcto, sin desbordamiento.

**c) $(-5) + (-4)$**

```text
   1011   (−5)
 + 1100   (−4)
 ------
 1 0111   -> 0111 = +7
```

El resultado exacto es $-9 < -8$, fuera del rango representable. Dos negativos produjeron un positivo: **hay desbordamiento**.

---

## Bloque D. Códigos

### Ejercicio 1.8

**a)** $359_{10}$:

$$
3 \to 0011 \qquad 5 \to 0101 \qquad 9 \to 1001 \qquad \Rightarrow \qquad 0011\,0101\,1001_{\text{BCD}}
$$

**b)** No es válida: el nibble $1100$ equivale a 12, y en BCD las combinaciones $1010$ a $1111$ no se utilizan.

**c)** Código Gray de 4 bits por el método del espejo. Las posiciones 0 a 7 son el Gray de 3 bits precedido de 0:

| Posición | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    |
|:--------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| Gray     | 0000 | 0001 | 0011 | 0010 | 0110 | 0111 | 0101 | 0100 |

Las posiciones 8 a 15 son el espejo de las anteriores precedido de 1; por tanto, la posición 8 es el espejo de la posición 7: $1\,100 = 1100$.

| Transición $7 \to 8$ | Valores           | Bits que cambian |
|:--------------------:|:-----------------:|:----------------:|
| Binario natural      | $0111 \to 1000$   | 4                |
| Gray                 | $0100 \to 1100$   | 1                |

### Ejercicio 1.9

**a)** Con $A = 65$: $U$ es la letra de índice 20, $N$ la de índice 13 y $L$ la de índice 11 (contando desde $A = 0$).

| Carácter | Cálculo        | Decimal | Hexadecimal |
|:--------:|:--------------:|:-------:|:-----------:|
| U        | $65 + 20$      | 85      | 0x55        |
| N        | $65 + 13$      | 78      | 0x4E        |
| L        | $65 + 11$      | 76      | 0x4C        |

**b)** $\mathrm{0x43} = 67 \rightarrow \text{C}$; $\mathrm{0x4F} = 79 \rightarrow \text{O}$; $\mathrm{0x44} = 68 \rightarrow \text{D}$; $\mathrm{0x45} = 69 \rightarrow \text{E}$. La secuencia es **«CODE»**.

---

## Bloque E. Compuertas lógicas

### Ejercicio 1.10

| Enunciado | Compuerta | Justificación |
|:---------:|:---------:|---------------|
| a | **AND** | Salida activa solo si ambas entradas están activas |
| b | **OR**  | Salida activa si al menos una entrada está activa |
| c | **XOR** | Salida activa si las entradas son distintas |
| d | **NOT** | Salida $= \overline{\text{sensor}}$: se apaga cuando el sensor se activa |

### Ejercicio 1.11

**a) $Y = A\cdot B + \overline{C}$**

| Dec | $A$ | $B$ | $C$ | $A\cdot B$ | $\overline{C}$ | $Y$   |
|:---:|:---:|:---:|:---:|:----------:|:--------------:|:-----:|
| 0   | 0   | 0   | 0   | 0          | 1              | **1** |
| 1   | 0   | 0   | 1   | 0          | 0              | 0     |
| 2   | 0   | 1   | 0   | 0          | 1              | **1** |
| 3   | 0   | 1   | 1   | 0          | 0              | 0     |
| 4   | 1   | 0   | 0   | 0          | 1              | **1** |
| 5   | 1   | 0   | 1   | 0          | 0              | 0     |
| 6   | 1   | 1   | 0   | 1          | 1              | **1** |
| 7   | 1   | 1   | 1   | 1          | 0              | **1** |

Con 3 entradas hay $2^3 = 8$ filas. Los minitérminos son $Y = \Sigma m(0, 2, 4, 6, 7)$.

**b) $Y = (A + B)\cdot\overline{C}$**

| Dec | $A$ | $B$ | $C$ | $A + B$ | $\overline{C}$ | $Y$   |
|:---:|:---:|:---:|:---:|:-------:|:--------------:|:-----:|
| 0   | 0   | 0   | 0   | 0       | 1              | 0     |
| 1   | 0   | 0   | 1   | 0       | 0              | 0     |
| 2   | 0   | 1   | 0   | 1       | 1              | **1** |
| 3   | 0   | 1   | 1   | 1       | 0              | 0     |
| 4   | 1   | 0   | 0   | 1       | 1              | **1** |
| 5   | 1   | 0   | 1   | 1       | 0              | 0     |
| 6   | 1   | 1   | 0   | 1       | 1              | **1** |
| 7   | 1   | 1   | 1   | 1       | 0              | 0     |

$Y = \Sigma m(2, 4, 6)$.

### Ejercicio 1.12

**a)** Alimentación: pin 14 ($V_{CC} = +5\ \text{V}$); tierra: pin 7 (GND). Compuerta 3: entradas 3A (pin 9) y 3B (pin 10); salida 3Y (pin 8).

**b)** `SN74LS08N`:

| Fragmento | Significado |
|:---------:|-------------|
| SN | Texas Instruments |
| 74 | Rango comercial |
| LS | Familia TTL |
| 08 | Cuatro compuertas AND de 2 entradas |
| N  | Encapsulado DIP de plástico |

**c)** Una entrada sin conectar queda en la zona indefinida (0,8 V a 2,0 V): el chip no garantiza si la lee como 0 o como 1, y el comportamiento del circuito puede ser errático.

**d)** Sí. El 74HC08 es la versión CMOS con la misma función (4 AND de 2 entradas) y la misma distribución de pines que el 74LS08, por lo que puede sustituirlo.

---

[← Anterior: Ejercicios](./ejercicios.md) | [Siguiente semana: Álgebra de Boole →](../semana-02/resumen.md)
