# Semana 4: Soluciones

---

## Bloque A. Suma binaria

### Ejercicio 4.1

```text
 acarreo    1 1 1 0
              1 0 1 1   (11)
            + 0 1 1 0   ( 6)
            ---------
            1 0 0 0 1   (17)
```

| Columna | Suma               | Escribo | Llevo |
|:-------:|:------------------:|:-------:|:-----:|
| 0       | $1 + 0 = 1$        | 1       | 0     |
| 1       | $1 + 1 = 2$        | 0       | 1     |
| 2       | $0 + 1 + 1 = 2$    | 0       | 1     |
| 3       | $1 + 0 + 1 = 2$    | 0       | 1     |

Resultado: $10001_2 = 16 + 1 = 17$, que coincide con $11 + 6 = 17$. En un sumador de 4 bits se obtiene $S = 0001$ con $C_{out} = 1$ (el quinto bit).

### Ejercicio 4.2

```text
 acarreo    1 1 1 0
              0 1 1 1   (7)
            + 0 1 1 1   (7)
            ---------
              1 1 1 0
```

| Columna | Suma            | Escribo | Llevo |
|:-------:|:---------------:|:-------:|:-----:|
| 0       | $1 + 1 = 2$     | 0       | 1     |
| 1       | $1 + 1 + 1 = 3$ | 1       | 1     |
| 2       | $1 + 1 + 1 = 3$ | 1       | 1     |
| 3       | $0 + 0 + 1 = 1$ | 1       | 0     |

$S = 1110$, $C_{out} = 0$.

- **(a) Sin signo:** $1110_2 = 14$ ✓ (correcto: $7 + 7 = 14$).
- **(b) Con signo:** $1110_2 = -2$ ✗: $+14$ excede $+7$; hay **desbordamiento** ($C_3 = 1$, $C_4 = 0$, $V = 1$).

---

## Bloque B. Diseño del semisumador y del sumador completo

### Ejercicio 4.3

**a)**

| $A$ | $B$ | $C$ | $S$ |
|:---:|:---:|:---:|:---:|
| 0   | 0   | 0   | 0   |
| 0   | 1   | 0   | 1   |
| 1   | 0   | 0   | 1   |
| 1   | 1   | 1   | 0   |

**b)** $S = 1$ si $A \neq B$ $\Rightarrow S = A \oplus B$ (XOR). $C = 1$ solo si $A = B = 1$ $\Rightarrow C = A \cdot B$ (AND).

**c)** 2 compuertas (1 XOR + 1 AND) y **2 CI**: 7486 + 7408.

### Ejercicio 4.4

**a)** Tabla de verdad (ver sección 3.1 del resumen):

| $A$ | $B$ | $C_{in}$ | N.º de 1 | $C_{out}\,S$ |
|:---:|:---:|:--------:|:--------:|:------------:|
| 0   | 0   | 0        | 0        | 00           |
| 0   | 0   | 1        | 1        | 01           |
| 0   | 1   | 0        | 1        | 01           |
| 0   | 1   | 1        | 2        | 10           |
| 1   | 0   | 0        | 1        | 01           |
| 1   | 0   | 1        | 2        | 10           |
| 1   | 1   | 0        | 2        | 10           |
| 1   | 1   | 1        | 3        | 11           |

**b)** Mapa de $S$ (ajedrez, sin grupos) y de $C_{out}$ (tres grupos de dos):

| $S$: $C_{in} \backslash AB$ | 00 | 01 | 11 | 10 |
|:---------------------------:|:--:|:--:|:--:|:--:|
| **0**                       | 0  | 1  | 0  | 1  |
| **1**                       | 1  | 0  | 1  | 0  |

| $C_{out}$: $C_{in} \backslash AB$ | 00 | 01 | 11 | 10 |
|:---------------------------------:|:--:|:--:|:--:|:--:|
| **0**                             | 0  | 0  | 1  | 0  |
| **1**                             | 0  | 1  | 1  | 1  |

$$
S = A \oplus B \oplus C_{in} \qquad\qquad C_{out} = AB + A\,C_{in} + B\,C_{in}
$$

**c)** Comparación por sumador completo:

| Implementación de $C_{out}$ | Compuertas de $S$ | Compuertas de $C_{out}$ | Total |
|-----------------------------|:-----------------:|:-----------------------:|:-----:|
| $AB + AC_{in} + BC_{in}$ | 2 XOR | 3 AND2 + 2 OR2 (OR de 3 entradas) | **7** |
| $AB + C_{in}(A \oplus B)$ | 2 XOR | 2 AND2 + 1 OR2 (reutiliza $A \oplus B$) | **5** |

*Verificación de la forma alternativa:* en la fila $ABC_{in} = 101$, $AB = 0$ y $C_{in}(A\oplus B) = 1\cdot 1 = 1$ $\Rightarrow C_{out} = 1$ ✓; en $100$ resulta $0$ ✓; en $111$, $AB = 1$ $\Rightarrow 1$ ✓.

**Sumador de 4 bits con compuertas sueltas** (forma de 5 compuertas $\times$ 4 etapas): 8 XOR, 8 AND, 4 OR.

| Tipo | Cantidad | CI (compuertas por chip) |
|:----:|:--------:|:------------------------:|
| XOR  | 8 | 2 × 7486 (4 por chip) |
| AND  | 8 | 2 × 7408 (4 por chip) |
| OR   | 4 | 1 × 7432 (4 por chip) |

Total: **5 CI** con compuertas sueltas, frente a 1 solo CI con el integrado sumador 7483 de 4 bits.

### Ejercicio 4.5

$A = 0110$ ($A_3A_2A_1A_0$) y $B = 0111$:

| Etapa | $A$ | $B$ | $C_{in}$ | N.º de 1 | $S$ | $C_{out}$ |
|:-----:|:---:|:---:|:--------:|:--------:|:---:|:---------:|
| 0     | 0   | 1   | 0        | 1        | 1   | 0         |
| 1     | 1   | 1   | 0        | 2        | 0   | 1         |
| 2     | 1   | 1   | 1        | 3        | 1   | 1         |
| 3     | 0   | 0   | 1        | 1        | 1   | 0         |

Resultado: $S_3S_2S_1S_0 = 1101 = 13$ ✓ ($6 + 7 = 13$).

---

## Bloque C. Retardo de propagación

### Ejercicio 4.6

$t \approx 2 \cdot n \cdot 10\ \text{ns}$:

| Bits $n$ | Cálculo | Retardo |
|:--------:|:-------:|:-------:|
| 8        | $2 \cdot 8 \cdot 10$  | 160 ns |
| 16       | $2 \cdot 16 \cdot 10$ | **320 ns** |
| 32       | $2 \cdot 32 \cdot 10$ | 640 ns |

**b)** Se exige $2 \cdot n \cdot 10 \leq 200 \Rightarrow n \leq 10$. El sumador puede tener como máximo **10 bits**.

---

## Bloque D. Resta con el sumador

### Ejercicio 4.7

Con $M = 1$: cada bit de $B$ pasa por una XOR con 1 (se invierte) y $C_{in} = 1$.

```text
 B   = 0011  (3)
 B'  = 1100  (invertido por las XOR)
 Cin = 1     (aporta el +1)

   0110   (A = 6)
 + 1100   (B invertido)
 +    1   (Cin)
 -------
 1 0011   -> se descarta el bit sobrante -> 0011 = 3
```

| Etapa | $A$ | $B \oplus M$ | $C_{in}$ | $S$ | $C_{out}$ |
|:-----:|:---:|:------------:|:--------:|:---:|:---------:|
| 0     | 0   | 0            | 1        | 1   | 0         |
| 1     | 1   | 0            | 0        | 1   | 0         |
| 2     | 1   | 1            | 0        | 0   | 1         |
| 3     | 0   | 1            | 1        | 0   | 1         |

Resultado: $0011 = 3$ ✓ ($6 - 3 = 3$).

### Ejercicio 4.8

$0101 - 0111$: $B = 0111 \to \overline{B} = 1000$, $C_{in} = 1$.

| Etapa | $A$ | $B \oplus M$ | $C_{in}$ | $S$ | $C_{out}$ |
|:-----:|:---:|:------------:|:--------:|:---:|:---------:|
| 0     | 1   | 0            | 1        | 0   | 1         |
| 1     | 0   | 0            | 1        | 1   | 0         |
| 2     | 1   | 0            | 0        | 1   | 0         |
| 3     | 0   | 1            | 0        | 1   | 0         |

$S = 1110 = -8 + 4 + 2 = -2$ ✓ ($5 - 7 = -2$). El acarreo de salida es 0: en una resta con este circuito, $C_{out} = 0$ indica que no hubo «bit sobrante» que descartar, es decir, que $A < B$ si se interpretan los operandos sin signo ($5 < 7$). Con signo, el resultado $-2$ es válido, pues $V = C_3 \oplus C_4 = 0 \oplus 0 = 0$.

---

## Bloque E. Desbordamiento

### Ejercicio 4.9

**a) $0101 + 0100$**

| Columna | $A$ | $B$ | $C_{in}$ | $S$ | Acarreo de salida |
|:-------:|:---:|:---:|:--------:|:---:|:-----------------:|
| 0       | 1   | 0   | 0        | 1   | 0 |
| 1       | 0   | 0   | 0        | 0   | 0 |
| 2       | 1   | 1   | 0        | 0   | 1 |
| 3       | 0   | 0   | 1        | 1   | 0 |

$S = 1001$, $C_{out} = C_4 = 0$, $C_3 = 1$ $\Rightarrow V = 1 \oplus 0 = 1$: **overflow** ($+9$ no cabe; se lee $-7$).

**b) $1011 + 1010$** ($-5 + (-6) = -11$)

| Columna | $A$ | $B$ | $C_{in}$ | $S$ | Acarreo de salida |
|:-------:|:---:|:---:|:--------:|:---:|:-----------------:|
| 0       | 1   | 0   | 0        | 1   | 0 |
| 1       | 1   | 1   | 0        | 0   | 1 |
| 2       | 0   | 0   | 1        | 1   | 0 |
| 3       | 1   | 1   | 0        | 0   | 1 |

$S = 0101$, $C_4 = 1$, $C_3 = 0$ $\Rightarrow V = 0 \oplus 1 = 1$: **overflow** ($-11 < -8$; se lee $+5$).

**c) $1110 + 0011$** ($-2 + 3 = 1$)

| Columna | $A$ | $B$ | $C_{in}$ | $S$ | Acarreo de salida |
|:-------:|:---:|:---:|:--------:|:---:|:-----------------:|
| 0       | 0   | 1   | 0        | 1   | 0 |
| 1       | 1   | 1   | 0        | 0   | 1 |
| 2       | 1   | 0   | 1        | 0   | 1 |
| 3       | 1   | 0   | 1        | 0   | 1 |

$S = 0001 = +1$ ✓, $C_4 = 1$, $C_3 = 1$ $\Rightarrow V = 1 \oplus 1 = 0$: **sin overflow**.

| Caso | $S$ | $C_3$ | $C_4 = C_{out}$ | $V$ |
|:----:|:---:|:-----:|:---------------:|:---:|
| a    | 1001 | 1 | 0 | **1** |
| b    | 0101 | 0 | 1 | **1** |
| c    | 0001 | 1 | 1 | 0 |

**Reflexión:** en (c), el 1 que sale por la izquierda es el bit sobrante habitual del complemento a dos (igual que al restar $6 - 3$), y el resultado $+1$ es correcto. El criterio de desbordamiento no es el valor de $C_{out}$, sino que el acarreo que entra a la última etapa difiera del que sale. Nótese que en (b) $C_{out} = 1$ y sí hay error, mientras que en (c) $C_{out} = 1$ y no lo hay.

---

## Bloque F. Comparador de magnitud

### Ejercicio 4.10

$A = 10$ ($A_1 = 1$, $A_0 = 0$), $B = 01$ ($B_1 = 0$, $B_0 = 1$).

- Bit alto: $A_1 = 1 > B_1 = 0$, el primer bit que difiere decide $\Rightarrow$ **$A > B$ es verdadero** ($2 > 1$).
- Igualdad: $A_1 \odot B_1 = 0 \Rightarrow (A = B) = 0$: **$A = B$ es falso**.

### Ejercicio 4.11

$$
(A > B) = A_1\overline{B_1} + (A_1 \odot B_1)\,A_0\overline{B_0} \qquad (A = B) = (A_1 \odot B_1)(A_0 \odot B_0)
$$

**a) $A = 11,\ B = 10$:** $A_1\overline{B_1} = 1\cdot 0 = 0$; $A_1 \odot B_1 = 1$ y $A_0\overline{B_0} = 1\cdot 1 = 1$ $\Rightarrow (A > B) = 0 + 1\cdot 1 = 1$. Igualdad: $(1)(0) = 0$. Por tanto $A > B$ ($3 > 2$).

**b) $A = 01,\ B = 01$:** $A_1\overline{B_1} = 0$; $A_1 \odot B_1 = 1$, $A_0\overline{B_0} = 1\cdot 0 = 0$ $\Rightarrow (A > B) = 0$. Igualdad: $(1)(1) = 1$. Por tanto $A = B$.

### Ejercicio 4.12

$$
(A = B) = (A_3 \odot B_3)(A_2 \odot B_2)(A_1 \odot B_1)(A_0 \odot B_0)
$$

Se requieren **4 compuertas XNOR** (una por par de bits) y **una AND de 4 entradas** (o 3 AND de 2 entradas en cascada). Total: 5 compuertas (o 7 si solo hay AND de 2 entradas).

---

[← Anterior: Ejercicios](./ejercicios.md) | [Volver al inicio del libro →](../README.md)
