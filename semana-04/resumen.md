# Semana 4: Circuitos aritméticos

**Unidad 1 · Lógica combinacional con diseño clásico**
**Tema:** semisumador, sumador completo, sumador de 4 bits, resta, desbordamiento y comparador
**Resultado de aprendizaje R1:** diseña circuitos combinacionales básicos utilizando técnicas de diseño clásico.

## Objetivos de la semana

Al finalizar el estudio de este capítulo, el lector podrá diseñar, con el procedimiento clásico, un circuito que suma números binarios de 4 bits, utilizarlo también para restar y estimar cuánto tarda en entregar el resultado. Específicamente:

- Deducir las funciones del semisumador y del sumador completo a partir de su tabla de verdad.
- Interconectar sumadores completos para formar un sumador de $n$ bits (acarreo en cascada).
- Estimar el retardo de propagación del acarreo.
- Realizar restas con el sumador mediante complemento a dos.
- Detectar el desbordamiento en aritmética con signo.
- Diseñar un comparador de magnitud.

> **Contexto:** estos circuitos son el corazón de la unidad aritmético-lógica (ALU) de un procesador.

---

## 1. Suma de un solo bit

La suma de dos bits tiene solo cuatro casos:

| Operación | Resultado | Se escribe ($S$) | Se lleva ($C$) |
|:---------:|:---------:|:----------------:|:--------------:|
| $0 + 0$   | $0$       | 0                | 0              |
| $0 + 1$   | $1$       | 1                | 0              |
| $1 + 0$   | $1$       | 1                | 0              |
| $1 + 1$   | $2 = 10_2$| 0                | 1              |

- **$S$ (suma):** el dígito que se escribe.
- **$C$ (carry, acarreo):** el que «se lleva».

> **Analogía decimal:** $7 + 5 = 12$: se escribe 2 y se lleva 1.

### 1.1 Ejemplo: $0110 + 0111$, columna por columna

```text
 acarreo    1 1 0 0
              0 1 1 0   ( 6)
            + 0 1 1 1   ( 7)
            ---------
              1 1 0 1   (13)
```

| Columna | Suma          | Escribo | Llevo |
|:-------:|:-------------:|:-------:|:-----:|
| 0       | $0 + 1 = 1$   | 1       | 0     |
| 1       | $1 + 1 = 2$   | 0       | 1     |
| 2       | $1 + 1 + 1 = 3$ | 1     | 1     |
| 3       | $0 + 0 + 1 = 1$ | 1     | 0     |

### 1.2 El acarreo puede aparecer en cualquier columna y encadenarse

```text
 acarreo    1 1 1 0
              0 1 1 1   (7)
            + 0 0 0 1   (1)
            ---------
              1 0 0 0   (8)
```

Un acarreo provoca otro: **los acarreos se encadenan**.

### 1.3 Dos tipos de columna, dos circuitos

| Columna                  | Bits que se suman                           | Circuito             |
|--------------------------|---------------------------------------------|:--------------------:|
| Columna 0                | 2 bits: $A$ y $B$ (a su derecha no hay nada) | **Semisumador**      |
| Columnas 1, 2, 3, …      | 3 bits: $A$, $B$ y el acarreo que llega ($C_{in}$) | **Sumador completo** |

---

## 2. Semisumador

### 2.1 Tabla de verdad

| $A$ | $B$ | $C$ | $S$ |
|:---:|:---:|:---:|:---:|
| 0   | 0   | 0   | 0   |
| 0   | 1   | 0   | 1   |
| 1   | 0   | 0   | 1   |
| 1   | 1   | 1   | 0   |

- La columna $S$ vale 1 cuando $A$ y $B$ son **distintos** $\Rightarrow$ compuerta XOR.
- La columna $C$ vale 1 solo cuando $A$ y $B$ son **ambos 1** $\Rightarrow$ compuerta AND.

$$
S = A \oplus B \qquad\qquad C = A\cdot B
$$

![Circuito del semisumador con una compuerta XOR para la suma y una compuerta AND para el acarreo](./assets/semisumador.png)

*Figura 4.1: Semisumador: una XOR produce la suma $S$ y una AND produce el acarreo $C$.*

> **Nota:** «semi» significa que el circuito no puede recibir acarreo; por ello solo sirve para la columna 0.

---

## 3. Sumador completo

### 3.1 El truco de contar unos

Se cuenta el número de unos en la fila y se escribe en binario como $C_{out}\,S$:

| $A$ | $B$ | $C_{in}$ | N.º de 1 | Binario | $C_{out}$ | $S$ |
|:---:|:---:|:--------:|:--------:|:-------:|:---------:|:---:|
| 0   | 0   | 0        | 0        | 00      | 0         | 0   |
| 0   | 0   | 1        | 1        | 01      | 0         | 1   |
| 0   | 1   | 0        | 1        | 01      | 0         | 1   |
| 0   | 1   | 1        | 2        | 10      | 1         | 0   |
| 1   | 0   | 0        | 1        | 01      | 0         | 1   |
| 1   | 0   | 1        | 2        | 10      | 1         | 0   |
| 1   | 1   | 0        | 2        | 10      | 1         | 0   |
| 1   | 1   | 1        | 3        | 11      | 1         | 1   |

En palabras:

- **$S = 1$** cuando hay un número **impar** de unos (1 o 3).
- **$C_{out} = 1$** cuando hay **al menos dos** unos (la mayoría).

### 3.2 Mapa de Karnaugh de $S$: el «tablero de ajedrez»

| $C_{in} \backslash AB$ | 00 | 01 | 11 | 10 |
|:----------------------:|:--:|:--:|:--:|:--:|
| **0**                  | 0  | 1  | 0  | 1  |
| **1**                  | 1  | 0  | 1  | 0  |

Los unos están alternados: **ningún 1 tiene vecino**, no hay grupos posibles. Un patrón de ajedrez indica una función XOR:

$$
S = A \oplus B \oplus C_{in}
$$

### 3.3 Mapa de Karnaugh de $C_{out}$: tres grupos de dos

| $C_{in} \backslash AB$ | 00 | 01 | 11 | 10 |
|:----------------------:|:--:|:--:|:--:|:--:|
| **0**                  | 0  | 0  | 1  | 0  |
| **1**                  | 0  | 1  | 1  | 1  |

| Grupo | Celdas | Término |
|:-----:|:------:|:-------:|
| Columna $AB = 11$ | $m_6, m_7$ | $AB$ |
| Fila $C_{in} = 1$, columnas 01 y 11 | $m_3, m_7$ | $B\cdot C_{in}$ |
| Fila $C_{in} = 1$, columnas 11 y 10 | $m_7, m_5$ | $A\cdot C_{in}$ |

$$
C_{out} = AB + A\,C_{in} + B\,C_{in} \qquad (\text{al menos dos unos})
$$

> **Forma alternativa:** $C_{out} = AB + C_{in}(A \oplus B)$. Reutiliza la XOR ya necesaria para $S$ y permite implementar el sumador completo con 2 XOR, 2 AND y 1 OR (5 compuertas).

![Sumador completo construido con dos semisumadores y una compuerta OR](./assets/sumador-completo.png)

*Figura 4.2: Sumador completo con entradas $A$, $B$, $C_{in}$ y salidas $S$ y $C_{out}$.*

### 3.4 ¿Hay que memorizar las fórmulas? No

| Paso | Acción |
|:----:|--------|
| 1 | Construir la **tabla de verdad** contando los unos |
| 2 | Aplicar el **mapa de Karnaugh**; si sale ajedrez $\Rightarrow$ XOR |
| 3 | Obtener la **expresión** y leerla en palabras |

> **Lo que se recuerda:** $S$ = impar de unos; $C_{out}$ = al menos dos unos.

---

## 4. Sumador de 4 bits con acarreo en cascada (*ripple carry*)

Se conectan cuatro sumadores completos con una única regla: **$C_{out}$ de un sumador $\rightarrow$ $C_{in}$ del siguiente**. En la etapa 0 el acarreo de entrada es 0 (o un semisumador).

![Sumador de 4 bits formado por cuatro sumadores completos conectados en cascada](./assets/sumador-4-bits-ripple.png)

*Figura 4.3: Sumador de 4 bits con acarreo en cascada. Entradas $A_3A_2A_1A_0$ y $B_3B_2B_1B_0$; salidas $S_3S_2S_1S_0$ y el acarreo final.*

### 4.1 Retardo de propagación

Cada sumador espera el acarreo del anterior, de modo que el resultado se completa **de derecha a izquierda**, como una ola (*ripple*).

![Propagación del acarreo: la etapa 0 queda lista en t1, la etapa 1 en t2, la etapa 2 en t3 y la etapa 3 en t4](./assets/propagacion-acarreo-ripple.png)

*Figura 4.4: Propagación del acarreo a través de las etapas del sumador.*

Supuestos: cada compuerta tarda $\approx 10$ ns y el acarreo cruza $\approx 2$ compuertas por etapa. Para $n$ bits:

$$
t_{\text{retardo}} \approx 2 \cdot n \cdot 10\ \text{ns}
$$

| Bits $n$ | Compuertas en la ruta del acarreo ($2n$) | Tiempo aproximado |
|:--------:|:----------------------------------------:|:-----------------:|
| 4        | 8                                        | 80 ns             |
| 16       | 32                                       | 320 ns            |
| 32       | 64                                       | 640 ns            |

> **Conclusión:** más bits $\Rightarrow$ más lento. El retardo crece linealmente con $n$.

---

## 5. La resta con el sumador

La resta se reduce a una suma con el negativo (complemento a dos, Semana 1):

$$
A - B = A + (-B) \qquad\qquad -B = \overline{B} + 1
$$

Ejemplo, $6 - 3$:

```text
 B   = 0011  (3)
 inv = 1100
 +1  = 1101  (−3)

   0110  (6)
 + 1101  (−3)
 -------
 1 0011  -> se descarta el 1 sobrante -> 0011 = 3
```

### 5.1 La XOR como inversor controlado

| $M$ | $B$ | $B \oplus M$ | Efecto |
|:---:|:---:|:------------:|--------|
| 0   | 0   | 0            | $M = 0$: $B$ pasa igual $\Rightarrow$ **SUMA** |
| 0   | 1   | 1            |        |
| 1   | 0   | 1            | $M = 1$: $B$ se invierte $\Rightarrow$ **RESTA** |
| 1   | 1   | 0            |        |

Además, la señal $M$ se conecta al $C_{in}$ del sumador 0, aportando el «+1» del complemento a dos.

![Sumador/restador de 4 bits: una XOR por cada bit de B controlada por la señal M, que también alimenta el acarreo de entrada](./assets/sumador-restador.png)

*Figura 4.5: Sumador/restador de 4 bits. Con $M = 0$ el circuito suma; con $M = 1$ resta.*

> **Resultado:** un solo circuito suma o resta según $M$.

---

## 6. Desbordamiento (*overflow*)

Con 4 bits y signo el rango es de $-8$ a $+7$. Si el resultado no cabe, el circuito entrega un valor incorrecto:

```text
   0101  (+5)
 + 0100  (+4)
 -------
   1001  -> −7   (incorrecto)
```

> **Atención:** $C_{out} = 1$ **no** significa error. En aritmética con signo, el desbordamiento se detecta comparando el acarreo que **entra** a la última etapa con el que **sale** de ella:

$$
V = C_3 \oplus C_4
$$

donde $C_3$ es el acarreo de entrada a la etapa 3 y $C_4$ es el acarreo de salida de la etapa 3 ($C_{out}$ del sumador).

| Caso | $C_3$ | $C_4$ | $V$ | Interpretación |
|------|:-----:|:-----:|:---:|----------------|
| $5 + 4$ (ejemplo anterior) | 1 | 0 | **1** | Overflow |
| $(-2) + 3 = 1$ | 1 | 1 | 0 | Hay $C_{out} = 1$ pero **no** hay error |

---

## 7. Comparador de magnitud

### 7.1 Igualdad: ¿$A = B$?

Se aplica una XNOR a cada par de bits (vale 1 si los bits son iguales) y se combinan con una AND. Para 2 bits:

$$
(A = B) = (A_1 \odot B_1)\cdot(A_0 \odot B_0)
$$

### 7.2 Mayor que: ¿$A > B$?

Se examina **desde la izquierda**: el primer bit en el que difieren decide. Para 2 bits, $A > B$ si $A$ gana en el bit alto, o empatan allí y $A$ gana en el bajo:

$$
(A > B) = A_1\overline{B_1} + (A_1 \odot B_1)\,A_0\overline{B_0}
$$

![Comparador de magnitud de 2 bits con compuertas XNOR, AND y OR](./assets/comparador-2-bits.png)

*Figura 4.6: Comparador de magnitud de 2 bits. El circuito integrado comercial equivalente es el 7485.*

---

## 8. De aquí sale la ALU

![Diagrama de bloques de una ALU: sumador/restador, comparador y bloque AND/OR/XOR conectados a un multiplexor que selecciona el resultado de la instrucción](./assets/alu-bloques.png)

*Figura 4.7: Bloques de una ALU: sumador/restador, comparador y compuertas lógicas AND/OR/XOR; un multiplexor (Semana 5) selecciona el resultado de la instrucción.*

---

## 9. Demostración: $0101 + 0011$ en el circuito

| Etapa | $A$ | $B$ | $C_{in}$ | N.º de 1 | $S$ | $C_{out}$ |
|:-----:|:---:|:---:|:--------:|:--------:|:---:|:---------:|
| 0     | 1   | 1   | 0        | 2        | 0   | 1         |
| 1     | 0   | 1   | 1        | 2        | 0   | 1         |
| 2     | 1   | 0   | 1        | 2        | 0   | 1         |
| 3     | 0   | 0   | 1        | 1        | 1   | 0         |

Resultado: $S_3S_2S_1S_0 = 1000 = 8$.

- **Sin signo:** $5 + 3 = 8$, correcto.
- **Con signo:** $C_3 = 1$ y $C_4 = 0$ $\Rightarrow V = 1$; el resultado $+8$ no cabe en 4 bits con signo (**overflow**).

---

## Resumen del capítulo

| Concepto        | Idea clave                                         |
|-----------------|----------------------------------------------------|
| Semisumador     | $S = A \oplus B$, $C = A\cdot B$; solo columna 0   |
| Sumador completo| $S$ = impar de unos; $C_{out}$ = al menos dos unos |
| Ripple          | El acarreo avanza etapa por etapa; $t \approx 2n \cdot 10$ ns |
| Resta           | $M = 1$: XOR invierte $B$ y $C_{in} = 1$           |
| Overflow        | $V = C_3 \oplus C_4$, no $C_{out}$                 |
| Comparador      | XNOR por bit para igualdad; decide el primer bit que difiere |

---

[← Anterior: Semana 3](../semana-03/soluciones.md) | [Siguiente: Ejercicios →](./ejercicios.md)
