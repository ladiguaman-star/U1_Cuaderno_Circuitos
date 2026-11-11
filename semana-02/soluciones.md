# Semana 2: Soluciones

---

## Bloque A. Leyes de De Morgan

### Ejercicio 2.1

**a)**
$$
\overline{A\cdot B\cdot C} = \overline{A} + \overline{B} + \overline{C}
$$

**b)**
$$
\overline{A + \overline{B}C} = \overline{A}\cdot\overline{\overline{B}C} = \overline{A}\,(B + \overline{C}) = \overline{A}B + \overline{A}\,\overline{C}
$$

**c)**
$$
\overline{\overline{A}B + C} = \overline{\overline{A}B}\cdot\overline{C} = (A + \overline{B})\,\overline{C} = A\overline{C} + \overline{B}\,\overline{C}
$$

**d)**
$$
\overline{\overline{A} + BC} = A\cdot\overline{BC} = A(\overline{B} + \overline{C}) = A\overline{B} + A\overline{C}
$$

*Verificación de (b)* con $A=0, B=0, C=0$: original $\overline{0 + 1\cdot 0} = 1$; resultado $0'\cdot 0 + 0'\cdot 0' = 0 + 1 = 1$ ✓.

---

## Bloque B. Minitérminos y maxitérminos

### Ejercicio 2.2

**a)** La fila 4 es $ABC = 100$:

$$
m_4 = A\overline{B}\,\overline{C} \qquad M_4 = \overline{A} + B + C
$$

Por De Morgan: $\overline{m_4} = \overline{A} + B + C = M_4$ ✓.

**b)** Fila 5 $= 101$: $m_5 = A\overline{B}C$. Fila 2 $= 010$: $M_2 = A + \overline{B} + C$.

**c)** Las filas 0 a 7 que no están en $\Sigma m(1, 2, 4, 7)$ son $0, 3, 5, 6$:

$$
F = \prod M(0, 3, 5, 6)
$$

---

## Bloque C. Teoremas y simplificación algebraica

### Ejercicio 2.3

**a)**

$$
\begin{aligned}
A + \overline{A}B &= (A + \overline{A})(A + B) && \text{distributiva (forma dual)} \\
                  &= 1\cdot(A + B)             && \text{complemento} \\
                  &= A + B                     && \text{identidad}
\end{aligned}
$$

**b)**

$$
\begin{aligned}
AB + A\overline{B} + \overline{A}B &= A(B + \overline{B}) + \overline{A}B && \text{factor común } A \\
                                   &= A + \overline{A}B                   && \text{complemento e identidad} \\
                                   &= A + B                               && \text{absorción del complemento}
\end{aligned}
$$

**c)**

$$
\begin{aligned}
(A + B)(A + C) &= AA + AC + AB + BC && \text{distributiva} \\
               &= A + AC + AB + BC  && \text{idempotencia} \\
               &= A(1 + C + B) + BC && \text{factor común} \\
               &= A + BC            && \text{elemento nulo}
\end{aligned}
$$

### Ejercicio 2.4

**a)** $F = A + \overline{A}B + A\overline{B}C$

$$
\begin{aligned}
F &= (A + B) + A\overline{B}C && A + \overline{A}B = A + B \\
  &= A + A\overline{B}C + B   && \text{conmutativa} \\
  &= A + B                    && \text{absorción}
\end{aligned}
$$

*Verificación* con $A=0, B=0, C=1$: original $= 0 + 0 + 0 = 0$; simplificada $= 0 + 0 = 0$ ✓.

**b)** $F = AB + \overline{A}C + BC$. Por el teorema del consenso ($XY + X'Z + YZ = XY + X'Z$ con $X = A$, $Y = B$, $Z = C$):

$$
F = AB + \overline{A}C
$$

**c)** $F = \overline{A}BC + A\overline{B}C + ABC + AB\overline{C} = \Sigma m(3, 5, 6, 7)$, la función de la alarma. Duplicando $ABC$ tres veces:

$$
F = (\overline{A}BC + ABC) + (A\overline{B}C + ABC) + (AB\overline{C} + ABC) = BC + AC + AB
$$

---

## Bloque D. Interpretación del enunciado

### Ejercicio 2.5

**Variables:** $C = 1$ si el control está presionado; $S = 1$ si el sensor indica obstáculo libre; $L = 1$ si la llave maestra está girada. Orden $C, S, L$.

**Interpretación:** $F = C\cdot S + L$ (la conjunción tiene precedencia sobre la disyunción).

| $i$ | $C$ | $S$ | $L$ | $C\cdot S$ | $F$   |
|:---:|:---:|:---:|:---:|:----------:|:-----:|
| 0   | 0   | 0   | 0   | 0          | 0     |
| 1   | 0   | 0   | 1   | 0          | **1** |
| 2   | 0   | 1   | 0   | 0          | 0     |
| 3   | 0   | 1   | 1   | 0          | **1** |
| 4   | 1   | 0   | 0   | 0          | 0     |
| 5   | 1   | 0   | 1   | 0          | **1** |
| 6   | 1   | 1   | 0   | 1          | **1** |
| 7   | 1   | 1   | 1   | 1          | **1** |

$$
F = \Sigma m(1, 3, 5, 6, 7) = \prod M(0, 2, 4)
$$

La forma simplificada ya está en el enunciado: $F = CS + L$. En POS: $M_0 M_2 M_4 = (C+S+L)(C+\overline{S}+L)(\overline{C}+S+L)$; los pares adyacentes dan $(C + L)(S + L) = L + CS$ ✓.

**Costo:** 1 AND + 1 OR = 2 compuertas, **2 CI** (7408 + 7432).

### Ejercicio 2.6

$F = 1$ solo en las filas 0 y 7:

$$
F = \Sigma m(0, 7) = \overline{A}\,\overline{B}\,\overline{C} + ABC
$$

$$
F = \prod M(1, 2, 3, 4, 5, 6)
$$

La SOP tiene solo 2 términos, mientras que la POS canónica requiere 6 sumas de 3 literales. Con la SOP la implementación natural sería NAND-NAND. Si solo se dispone de compuertas **NOR**, la forma natural es POS (NOR-NOR); en ese caso conviene simplificar la POS antes de implementar. Una forma equivalente es

$$
F = (\overline{A} + B)(\overline{B} + C)(\overline{C} + A),
$$

que expresa «$A \Rightarrow B$, $B \Rightarrow C$ y $C \Rightarrow A$», es decir, las tres variables son iguales. *Verificación:* vale 1 en $000$ y $111$, y 0 en las otras seis combinaciones.

---

## Bloque E. Taller de diseño por grupos

### Problema 2.7: Luz de pasillo

$F = 1$ cuando $A \neq B$ **y** $M = 0$.

| $i$ | $A$ | $B$ | $M$ | $F$   |
|:---:|:---:|:---:|:---:|:-----:|
| 0   | 0   | 0   | 0   | 0     |
| 1   | 0   | 0   | 1   | 0     |
| 2   | 0   | 1   | 0   | **1** |
| 3   | 0   | 1   | 1   | 0     |
| 4   | 1   | 0   | 0   | **1** |
| 5   | 1   | 0   | 1   | 0     |
| 6   | 1   | 1   | 0   | 0     |
| 7   | 1   | 1   | 1   | 0     |

$$
F = \Sigma m(2, 4) = \prod M(0, 1, 3, 5, 6, 7)
$$

$$
F_{\text{can}} = \overline{A}B\overline{M} + A\overline{B}\,\overline{M} = \overline{M}(\overline{A}B + A\overline{B}) = \overline{M}\,(A \oplus B)
$$

| Versión      | Compuertas                          | CI                      |
|--------------|-------------------------------------|-------------------------|
| Canónica     | 3 NOT + 2 AND3 + 1 OR2 = 6          | 7404 + 7411 + 7432 (3)  |
| Simplificada | 1 XOR + 1 NOT + 1 AND2 = 3          | 7486 + 7404 + 7408 (3)  |

> **Nota:** el número de CI coincide, pero la versión simplificada usa la mitad de compuertas y deja espacio libre en cada chip.

### Problema 2.8: Detector de primos

Los números primos entre 0 y 7 son 2, 3, 5 y 7 (el 0 y el 1 no son primos).

| $i$ | $A$ | $B$ | $C$ | $F$   |
|:---:|:---:|:---:|:---:|:-----:|
| 0   | 0   | 0   | 0   | 0     |
| 1   | 0   | 0   | 1   | 0     |
| 2   | 0   | 1   | 0   | **1** |
| 3   | 0   | 1   | 1   | **1** |
| 4   | 1   | 0   | 0   | 0     |
| 5   | 1   | 0   | 1   | **1** |
| 6   | 1   | 1   | 0   | 0     |
| 7   | 1   | 1   | 1   | **1** |

$$
F = \Sigma m(2, 3, 5, 7) = \prod M(0, 1, 4, 6)
$$

$$
\begin{aligned}
F_{\text{can}} &= \overline{A}B\overline{C} + \overline{A}BC + A\overline{B}C + ABC \\
&= \overline{A}B(\overline{C} + C) + AC(\overline{B} + B) = \overline{A}B + AC
\end{aligned}
$$

En POS: $M_0M_1 = A + B$ y $M_4M_6 = \overline{A} + C$, de modo que $F = (A + B)(\overline{A} + C)$. Ambas formas son equivalentes (el término $BC$ del mapa completo es redundante por consenso).

| Versión              | Compuertas                    | CI                          |
|----------------------|-------------------------------|-----------------------------|
| Canónica             | 3 NOT + 4 AND3 + 3 OR2 = 10   | 7404 + 2 × 7411 + 7432 (4)  |
| Simplificada (SOP)   | 1 NOT + 2 AND2 + 1 OR2 = 4    | 7404 + 7408 + 7432 (3)      |

### Problema 2.9: Bomba de agua

**Interpretación:** $F = B\cdot(A + C)$ (agua en la cisterna **y** [tanque bajo **o** manual]).

| $i$ | $A$ | $B$ | $C$ | $F$   |
|:---:|:---:|:---:|:---:|:-----:|
| 0   | 0   | 0   | 0   | 0     |
| 1   | 0   | 0   | 1   | 0     |
| 2   | 0   | 1   | 0   | 0     |
| 3   | 0   | 1   | 1   | **1** |
| 4   | 1   | 0   | 0   | 0     |
| 5   | 1   | 0   | 1   | 0     |
| 6   | 1   | 1   | 0   | **1** |
| 7   | 1   | 1   | 1   | **1** |

$$
F = \Sigma m(3, 6, 7) = \prod M(0, 1, 2, 4, 5)
$$

$$
F_{\text{can}} = \overline{A}BC + AB\overline{C} + ABC = BC + AB = B(A + C)
$$

| Versión      | Compuertas                    | CI                   |
|--------------|-------------------------------|----------------------|
| Canónica     | 2 NOT + 3 AND3 + 2 OR2 = 7    | 7404 + 7411 + 7432 (3) |
| Simplificada | 1 OR2 + 1 AND2 = 2            | 7432 + 7408 (2)      |

> **Nota:** si se interpretara «(agua y tanque bajo) o manual», la función sería $F = AB + C$, con $\Sigma m(1, 3, 5, 6, 7)$. Por eso es indispensable declarar la interpretación.

### Problema 2.10: Aviso de cinturón

**Interpretación:** $F = E\cdot(\overline{C} + P)$, con $C = 1$ cuando el cinturón está puesto.

| $i$ | $E$ | $C$ | $P$ | $F$   |
|:---:|:---:|:---:|:---:|:-----:|
| 0   | 0   | 0   | 0   | 0     |
| 1   | 0   | 0   | 1   | 0     |
| 2   | 0   | 1   | 0   | 0     |
| 3   | 0   | 1   | 1   | 0     |
| 4   | 1   | 0   | 0   | **1** |
| 5   | 1   | 0   | 1   | **1** |
| 6   | 1   | 1   | 0   | 0     |
| 7   | 1   | 1   | 1   | **1** |

$$
F = \Sigma m(4, 5, 7) = \prod M(0, 1, 2, 3, 6)
$$

$$
\begin{aligned}
F_{\text{can}} &= E\overline{C}\,\overline{P} + E\overline{C}P + ECP \\
&= E\overline{C} + EP && \text{(duplicando } E\overline{C}P\text{ y aplicando adyacencia)} \\
&= E(\overline{C} + P)
\end{aligned}
$$

| Versión      | Compuertas                    | CI                     |
|--------------|-------------------------------|------------------------|
| Canónica     | 2 NOT + 3 AND3 + 2 OR2 = 7    | 7404 + 7411 + 7432 (3) |
| Simplificada | 1 NOT + 1 OR2 + 1 AND2 = 3    | 7404 + 7432 + 7408 (3) |

> **Nota:** si se define $C = 1$ cuando el cinturón **no** está puesto, la función es $F = E(C + P)$ y se elimina el inversor (2 compuertas, 2 CI).

---

## Ticket de salida

1. $\overline{\overline{A} + BC} = A\cdot\overline{BC} = A(\overline{B} + \overline{C}) = A\overline{B} + A\overline{C}$.
2. $m_4 = A\overline{B}\,\overline{C}$ y $M_4 = \overline{A} + B + C$.

---

[← Anterior: Ejercicios](./ejercicios.md) | [Siguiente semana: Mapas de Karnaugh, indiferentes y NAND/NOR →](../semana-03/resumen.md)
