# Semana 1: Sistemas numéricos, códigos y compuertas lógicas

**Unidad 1 · Análisis de lógica combinacional con diseño clásico**
**Resultado de aprendizaje R1:** diseña e implementa circuitos combinacionales básicos utilizando técnicas de diseño clásico.

## Objetivos de la semana

Al finalizar el estudio de este capítulo, el lector podrá:

- Convertir números entre los sistemas decimal, binario, octal y hexadecimal.
- Representar números negativos en complemento a dos.
- Reconocer los códigos BCD, Gray y ASCII y su aplicación.
- Identificar las siete compuertas lógicas y ubicarlas en un circuito integrado de la familia 74LS.

---

## 1. Representación binaria de la información

Los sistemas digitales utilizan únicamente dos estados, denotados **0** y **1**, porque un transistor opera como un interruptor controlado por voltaje:

| Estado del interruptor | Corriente  | Nivel de voltaje | Símbolo |
|:----------------------:|:----------:|:----------------:|:-------:|
| Abierto                | No circula | Bajo             | 0       |
| Cerrado                | Circula    | Alto             | 1       |

Con solo dos estados resulta sencillo distinguir uno de otro, incluso cuando la señal llega contaminada por ruido eléctrico.

### 1.1 Niveles lógicos como rangos de voltaje

Un «1» o un «0» no corresponde a un voltaje exacto, sino a un **rango**. En la familia **74LS** (alimentación de 5 V) se definen los siguientes umbrales:

| Parámetro       | Descripción                                                  | Valor                  |
|-----------------|--------------------------------------------------------------|:----------------------:|
| $V_{OH}$ (mín.) | Voltaje que la compuerta emisora garantiza al entregar un 1  | $\geq 2{,}7\ \text{V}$ |
| $V_{IH}$ (mín.) | Voltaje a partir del cual la compuerta receptora lee un 1    | $\geq 2{,}0\ \text{V}$ |
| $V_{IL}$ (máx.) | Voltaje hasta el cual la compuerta receptora lee un 0        | $\leq 0{,}8\ \text{V}$ |
| $V_{OL}$ (máx.) | Voltaje que la compuerta emisora garantiza al entregar un 0  | $\leq 0{,}5\ \text{V}$ |

![Niveles de voltaje de salida y entrada de la familia 74LS, con la zona indefinida entre 0,8 V y 2,0 V](./assets/niveles-voltaje-74ls.png)

*Figura 1.1: Niveles de voltaje de salida (promesa del emisor) y de entrada (exigencia del receptor) en la familia 74LS.*

> **Nota:** Entre 0,8 V y 2,0 V se encuentra la **zona indefinida**: el circuito integrado no garantiza ninguna lectura y puede interpretar 0 o 1. Una causa frecuente es una entrada sin conectar.

### 1.2 Margen de ruido

El margen de ruido es la diferencia entre lo que el emisor garantiza y lo que el receptor exige:

$$
NM_H = V_{OH(\min)} - V_{IH(\min)} = 2{,}7 - 2{,}0 = 0{,}7\ \text{V}
$$

$$
NM_L = V_{IL(\max)} - V_{OL(\max)} = 0{,}8 - 0{,}5 = 0{,}3\ \text{V}
$$

![Márgenes de ruido alto (0,7 V) y bajo (0,3 V) en la familia 74LS](./assets/margen-ruido.png)

*Figura 1.2: Márgenes de ruido alto y bajo de la familia 74LS.*

> **Ejemplo de falla:** una compuerta entrega un 0 de 0,5 V y un motor cercano induce 0,4 V de ruido. Al receptor llegan 0,9 V, valor ubicado en la zona indefinida, y se produce un error de lectura.

---

## 2. Sistemas numéricos posicionales

En un sistema posicional el valor de un dígito depende de su **posición**, la cual representa una potencia de la base $r$. Para un número con $n$ dígitos enteros:

$$
N = \sum_{i=0}^{n-1} d_i \, r^{\,i}
$$

![Descomposición posicional del número 555 en centenas, decenas y unidades](./assets/sistema-posicional.png)

*Figura 1.3: Descomposición posicional del número decimal 555 ($500 + 50 + 5$).*

> **Nota:** Los números romanos no son posicionales: en XV la V vale 5 independientemente de su ubicación, lo que dificulta las operaciones aritméticas.

### 2.1 Sistema binario

En base 2 las posiciones valen $1, 2, 4, 8, 16, \dots$ Un **bit** es un dígito binario y un **byte** es un conjunto de 8 bits.

| Potencia | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
|:--------:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| Peso     | 128   | 64    | 32    | 16    | 8     | 4     | 2     | 1     |

Ejemplo: $1011_2 = 8 + 0 + 2 + 1 = 11_{10}$.

### 2.2 Conversión de decimal a binario

Se divide sucesivamente entre 2 y se leen los residuos **de abajo hacia arriba**.

| División    | Cociente | Residuo |
|:-----------:|:--------:|:-------:|
| $25 \div 2$ | 12       | 1       |
| $12 \div 2$ | 6        | 0       |
| $6 \div 2$  | 3        | 0       |
| $3 \div 2$  | 1        | 1       |
| $1 \div 2$  | 0        | 1       |

$$
25_{10} = 11001_2 \qquad \text{Comprobación: } 16 + 8 + 1 = 25
$$

### 2.3 Hexadecimal y octal como abreviaturas del binario

- **Hexadecimal (base 16):** se agrupan los bits de 4 en 4 desde la derecha.
- **Octal (base 8):** se agrupan los bits de 3 en 3 desde la derecha.
- Si falta algún bit, se completa con ceros a la izquierda.

| Dec | 10 | 11 | 12 | 13 | 14 | 15 |
|:---:|:--:|:--:|:--:|:--:|:--:|:--:|
| Hex | A  | B  | C  | D  | E  | F  |

$$
157_{10} = 1001\,1101_2 = 9\mathrm{D}_{16} \qquad 157_{10} = 010\,011\,101_2 = 235_8
$$

---

## 3. Aritmética binaria: la suma

Las reglas son las de la suma decimal, con acarreo:

| Operación   | Resultado                          |
|:-----------:|:----------------------------------:|
| $0 + 0$     | $0$                                |
| $0 + 1$     | $1$                                |
| $1 + 1$     | $10$ (se escribe 0 y se lleva 1)   |
| $1 + 1 + 1$ | $11$ (se escribe 1 y se lleva 1)   |

```text
 acarreo   1 1 1
           1 0 1 1   (11)
         + 0 1 1 0   ( 6)
         ---------
         1 0 0 0 1   (17)
```

---

## 4. Números con signo: complemento a dos

Un circuito no dispone del símbolo «−». Del mismo modo que un cuentakilómetros que retrocede desde 000 muestra 999, en binario de 4 bits se cumple $0000 - 1 = 1111$. Se acuerda entonces que $1111$ representa $-1$, $1110$ representa $-2$, y así sucesivamente. Ese acuerdo se denomina **complemento a dos**.

### 4.1 Valor de un número en complemento a dos

Para $n$ bits, el bit más significativo tiene peso negativo:

$$
N = -b_{n-1}\,2^{\,n-1} + \sum_{i=0}^{n-2} b_i\, 2^{\,i}
$$

Ejemplo: $1011_2 = -8 + 0 + 2 + 1 = -5$.

| Binario | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 |
|:-------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| Decimal | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    |

| Binario | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |
|:-------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| Decimal | −8   | −7   | −6   | −5   | −4   | −3   | −2   | −1   |

El rango representable con $n$ bits es:

$$
-2^{\,n-1} \;\leq\; N \;\leq\; 2^{\,n-1} - 1
$$

Con 4 bits: de $-8$ a $+7$; con 8 bits: de $-128$ a $+127$.

### 4.2 Obtención del negativo: invertir y sumar 1

Sea $\overline{X}$ el número $X$ con todos sus bits invertidos. Como $X + \overline{X} = 11\ldots1 = 2^n - 1$, se cumple $X + \overline{X} + 1 = 2^n \equiv 0 \pmod{2^n}$. Por tanto:

$$
-X = \overline{X} + 1
$$

![Procedimiento para obtener −3 a partir de 3: invertir bits y sumar 1](./assets/complemento-a-dos.png)

*Figura 1.4: Obtención de $-3$ en 4 bits: $0011 \rightarrow 1100 \rightarrow 1101$.*

Aplicación a la resta, $5 - 3 = 5 + (-3)$:

```text
   0101
 + 1101
 ------
 1 0010   -> se descarta el bit sobrante -> 0010 = 2
```

> **Nota:** La ventaja del complemento a dos es que **no se requiere un circuito restador**: el mismo sumador, con inversores, realiza la resta. El bit que excede a la izquierda se descarta.

### 4.3 Desbordamiento (overflow)

El resultado debe caber en los bits disponibles. Con 4 bits: $0111 + 0001 = 1000 = -8$ (incorrecto). Dos operandos positivos producen un resultado negativo, o viceversa. El mismo fenómeno ocurre con el tipo `int` de Java (32 bits): `2147483647 + 1` produce `-2147483648`. La detección por hardware se estudia en la Semana 4.

---

## 5. Códigos

### 5.1 BCD (decimal codificado en binario)

Cada dígito decimal se codifica con 4 bits. Las combinaciones `1010` a `1111` no se utilizan.

$$
157_{10} = \underbrace{0001}_{1}\ \underbrace{0101}_{5}\ \underbrace{0111}_{7}\ \text{(BCD)}
$$

El binario natural de 157 es $10011101_2$, que es una representación distinta. El BCD se emplea en displays: relojes, calculadoras y contadores.

### 5.2 Código Gray

Entre dos valores consecutivos cambia **un solo bit**. Se construye con el **método del espejo**: se copia la lista en orden inverso, se antepone 0 a la lista original y 1 a la copia.

| Posición      | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
|:-------------:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Gray (3 bits) | 000 | 001 | 011 | 010 | 110 | 111 | 101 | 100 |

![Construcción del código Gray de 1, 2 y 3 bits por el método del espejo](./assets/codigo-gray.png)

*Figura 1.5: Construcción del código Gray de 1, 2 y 3 bits mediante el método del espejo.*

En binario natural, el paso $3 \rightarrow 4$ ($011 \rightarrow 100$) modifica 3 bits simultáneamente, por lo que un sensor puede leer valores falsos durante la transición. Por ello el código Gray se usa en perillas y *encoders* rotativos. El orden $00, 01, 11, 10$ del mapa de Karnaugh (Semana 3) es un código Gray.

### 5.3 ASCII

Es una tabla acordada que asocia caracteres con números. Utiliza 7 bits, es decir, 128 caracteres (letras, dígitos, signos y controles).

| Carácter    | H    | O    | L    | A    |
|:-----------:|:----:|:----:|:----:|:----:|
| Decimal     | 72   | 79   | 76   | 65   |
| Hexadecimal | 0x48 | 0x4F | 0x4C | 0x41 |

![Codificación ASCII de la palabra HOLA en decimal y hexadecimal](./assets/ascii-hola.png)

*Figura 1.6: Codificación ASCII de la palabra «HOLA».*

Así, la letra «A» se almacena como $65_{10} = 01000001_2$. La «ñ» y las tildes no pertenecen a ASCII; para ellas existe UTF-8.

| Código | Aplicación principal                    | Característica                           |
|--------|-----------------------------------------|------------------------------------------|
| BCD    | Displays, contadores                    | 4 bits por dígito decimal                |
| Gray   | Sensores, *encoders*, mapas de Karnaugh | Un bit cambia entre valores consecutivos |
| ASCII  | Representación de texto                 | 7 bits, 128 caracteres                   |

---

## 6. Compuertas lógicas

### 6.1 Compuertas básicas

| Compuerta | Expresión           | Descripción                                   |
|-----------|:-------------------:|-----------------------------------------------|
| NOT       | $Y = \overline{A}$  | Invierte la entrada                           |
| AND       | $Y = A \cdot B$     | Vale 1 solo si **todas** las entradas valen 1 |
| OR        | $Y = A + B$         | Vale 1 si **al menos una** entrada vale 1     |

| $A$ | $Y_{NOT}$ |     | $A$ | $B$ | $Y_{AND}$ | $Y_{OR}$ |
|:---:|:---------:|:---:|:---:|:---:|:---------:|:--------:|
| 0   | 1         |     | 0   | 0   | 0         | 0        |
| 1   | 0         |     | 0   | 1   | 0         | 1        |
|     |           |     | 1   | 0   | 0         | 1        |
|     |           |     | 1   | 1   | 1         | 1        |

### 6.2 Compuertas negadas

El círculo en la salida del símbolo indica negación.

| $A$ | $B$ | NAND $\overline{A\cdot B}$ | NOR $\overline{A+B}$ |
|:---:|:---:|:--------------------------:|:--------------------:|
| 0   | 0   | 1                          | 1                    |
| 0   | 1   | 1                          | 0                    |
| 1   | 0   | 1                          | 0                    |
| 1   | 1   | 0                          | 0                    |

> **Nota:** Con solo compuertas NAND (o solo NOR) es posible construir cualquier circuito combinacional. Este resultado se desarrolla en la Semana 3.

### 6.3 Compuertas de comparación

| $A$ | $B$ | XOR $A \oplus B$ | XNOR $\overline{A \oplus B}$ |
|:---:|:---:|:----------------:|:----------------------------:|
| 0   | 0   | 0                | 1                            |
| 0   | 1   | 1                | 0                            |
| 1   | 0   | 1                | 0                            |
| 1   | 1   | 0                | 1                            |

- **XOR:** vale 1 si las entradas son **distintas**.
- **XNOR:** vale 1 si las entradas son **iguales**.
- Ejemplo cotidiano: la luz de una escalera con dos interruptores cambia cada vez que se acciona cualquiera de ellos; ese comportamiento es el de una XOR.

![Símbolos de las siete compuertas lógicas según ANSI/IEEE e IEC](./assets/simbolos-ansi-iec.png)

*Figura 1.7: Símbolos de las siete compuertas según la norma ANSI/IEEE (formas distintivas) y la norma IEC (rectángulos con símbolo).*

> **Nota:** En este curso se utiliza la norma ANSI. Si el simulador muestra rectángulos, se modifica en sus opciones.

---

## 7. Las compuertas como circuitos integrados: el 74LS08

El **74LS08** contiene cuatro compuertas AND de dos entradas en un encapsulado **DIP-14** (dos filas de 7 pines, apto para protoboard). La muesca se ubica arriba; el pin 1 queda arriba a la izquierda y la numeración avanza en sentido antihorario.

| Pin | Señal | Pin | Señal           |
|:---:|:-----:|:---:|:---------------:|
| 1   | 1A    | 14  | $V_{CC}$ (+5 V) |
| 2   | 1B    | 13  | 4B              |
| 3   | 1Y    | 12  | 4A              |
| 4   | 2A    | 11  | 4Y              |
| 5   | 2B    | 10  | 3B              |
| 6   | 2Y    | 9   | 3A              |
| 7   | GND   | 8   | 3Y              |

![Distribución de pines del circuito integrado 74LS08 en encapsulado DIP-14](./assets/pinout-74ls08.png)

*Figura 1.8: Distribución de pines del 74LS08 (vista superior): alimentación en el pin 14 y tierra en el pin 7.*

### 7.1 Lectura del código impreso: SN74LS08N

| Fragmento | Significado                                |
|:---------:|--------------------------------------------|
| SN        | Fabricante (Texas Instruments)             |
| 74        | Rango de uso comercial (54 = militar)      |
| LS        | Familia/tecnología (LS = TTL; HC = CMOS)   |
| 08        | Función: 4 compuertas AND de 2 entradas    |
| N         | Encapsulado DIP de plástico                |

> **Nota:** La hoja de datos se busca como «74LS08 datasheet», preferentemente en el sitio del fabricante (ti.com, onsemi.com). El **74HC08** tiene la misma función y la misma distribución de pines (versión CMOS) y puede utilizarse como sustituto.

---

## Resumen del capítulo

| Tema              | Idea clave                                                                       |
|-------------------|----------------------------------------------------------------------------------|
| Dos estados       | 0 y 1 son rangos de voltaje; entre ellos existe una zona indefinida              |
| Bases             | Binario = potencias de 2; hexadecimal = grupos de 4 bits; octal = grupos de 3 bits |
| Complemento a dos | $-X = \overline{X} + 1$; restar equivale a sumar el negativo                     |
| Códigos           | BCD para displays, Gray para sensores, ASCII para texto                          |
| Compuertas        | NOT, AND, OR, NAND, NOR, XOR y XNOR, con su tabla de verdad                      |
| Hoja de datos     | Pines, alimentación (14 y 7) y función del 74LS08                                |

---

[← Inicio del libro](../README.md) | [Siguiente: Ejercicios →](./ejercicios.md)
