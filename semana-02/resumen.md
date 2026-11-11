# Semana 2: Álgebra de Boole y formas canónicas

**Unidad 1 · Análisis de lógica combinacional con diseño clásico**
**Resultado de aprendizaje R1:** diseña e implementa circuitos combinacionales básicos utilizando técnicas de diseño clásico.

## Objetivos de la semana

Al finalizar el estudio de este capítulo, el lector podrá pasar de un enunciado a la tabla de verdad, a la forma canónica y a un circuito simplificado. Específicamente:

- Establecer la equivalencia entre un circuito y una expresión booleana.
- Aplicar los postulados, teoremas y leyes de De Morgan del álgebra de Boole.
- Obtener las formas canónicas SOP ($\Sigma m$) y POS ($\Pi M$) a partir de una tabla de verdad.
- Simplificar algebraicamente una expresión y cuantificar el ahorro en compuertas y circuitos integrados.

---

## 1. Circuito y expresión: una misma descripción

![Circuito de ejemplo con tres entradas A, B y C y una salida Y, correspondiente a la actividad APE 01](./assets/circuito-ejemplo-ape01.png)

*Figura 2.1: Circuito combinacional de tres entradas cuya expresión es $Y = A\cdot B + \overline{C}$.*

Todo circuito combinacional de compuertas admite una expresión booleana equivalente, y viceversa:

| Circuito                  | Expresión                |
|---------------------------|--------------------------|
| Cable de entrada          | Variable ($A$, $B$, $C$) |
| Compuerta AND             | Producto ($\cdot$)       |
| Compuerta OR              | Suma ($+$)               |
| Compuerta NOT             | Complemento ($\overline{\phantom{A}}$ o $'$) |
| Salida                    | Valor de la expresión    |

La **precedencia** de los operadores es: **NOT → AND → OR**. Así, $Y = A\cdot B + \overline{C}$ se evalúa calculando primero $\overline{C}$ y $A\cdot B$, y finalmente su suma.

---

## 2. Del enunciado a la especificación

Los enunciados en lenguaje natural suelen ser ambiguos; el primer paso del diseño es traducirlos a una tabla de verdad sin ambigüedad.

Considérese: *«La sirena suena cuando se activan dos sensores»*, con tres sensores $A$, $B$, $C$.

| Lectura          | Significado                    | Filas con $F = 1$   | Función                |
|------------------|--------------------------------|:-------------------:|:----------------------:|
| Exactamente dos  | Con los tres activos no suena  | 011, 101, 110       | $F = \Sigma m(3, 5, 6)$ |
| **Al menos dos** | Suena también con los tres     | 011, 101, 110, 111  | $F = \Sigma m(3, 5, 6, 7)$ |

> **Nota:** La segunda lectura (al menos dos) es la requerida por el cliente en el ejemplo de este capítulo.

---

## 3. Postulados de Huntington

El álgebra de Boole se define sobre el conjunto $\{0, 1\}$ con tres operaciones: $+$ (OR), $\cdot$ (AND) y $'$ (NOT).

| Postulado    | Forma OR                    | Forma AND (dual)             |
|--------------|:---------------------------:|:----------------------------:|
| Identidad    | $X + 0 = X$                 | $X \cdot 1 = X$              |
| Complemento  | $X + X' = 1$                | $X \cdot X' = 0$             |
| Conmutativa  | $X + Y = Y + X$             | $XY = YX$                    |
| Distributiva | $X(Y + Z) = XY + XZ$        | $X + YZ = (X + Y)(X + Z)$    |

> **Principio de dualidad:** si se intercambian $+ \leftrightarrow \cdot$ y $0 \leftrightarrow 1$ (sin complementar variables) en una identidad válida, se obtiene otra identidad válida.

---

## 4. Teoremas fundamentales

| Teorema                    | Forma OR                          | Forma AND                         |
|----------------------------|:---------------------------------:|:---------------------------------:|
| Elemento nulo              | $X + 1 = 1$                       | $X \cdot 0 = 0$                   |
| Idempotencia               | $X + X = X$                       | $X \cdot X = X$                   |
| Involución                 | $(X')' = X$                       | —                                 |
| Absorción                  | $X + XY = X$                      | $X(X + Y) = X$                    |
| Absorción del complemento  | $X + X'Y = X + Y$                 | $X(X' + Y) = XY$                  |
| Adyacencia                 | $XY + XY' = X$                    | $(X + Y)(X + Y') = X$             |
| Consenso                   | $XY + X'Z + YZ = XY + X'Z$        | $(X+Y)(X'+Z)(Y+Z) = (X+Y)(X'+Z)$ |

> **Nota:** La tabla se consulta y se aplica; no es necesario memorizarla. Las demostraciones siguientes ilustran el método.

### 4.1 Deducción de los teoremas más utilizados

**Adyacencia.**

$$
XY + XY' = X(Y + Y') = X \cdot 1 = X
$$

**Absorción.**

$$
X + XY = X(1 + Y) = X \cdot 1 = X
$$

**Absorción del complemento** (por la distributiva dual):

$$
X + X'Y = (X + X')(X + Y) = 1\cdot(X + Y) = X + Y
$$

**Consenso.** Se multiplica el término redundante por $(X + X') = 1$:

$$
\begin{aligned}
XY + X'Z + YZ &= XY + X'Z + YZ(X + X') \\
              &= XY + X'Z + XYZ + X'YZ \\
              &= XY(1 + Z) + X'Z(1 + Y) \\
              &= XY + X'Z
\end{aligned}
$$

### 4.2 La distributiva que sorprende: $A + BC = (A + B)(A + C)$

$$
\begin{aligned}
(A + B)(A + C) &= AA + AC + AB + BC && \text{distributiva} \\
               &= A + AC + AB + BC  && \text{idempotencia: } AA = A \\
               &= A(1 + C + B) + BC && \text{factor común } A \\
               &= A + BC            && \text{elemento nulo: } 1 + \cdots = 1
\end{aligned}
$$

---

## 5. Leyes de De Morgan

$$
\overline{A\cdot B} = \overline{A} + \overline{B} \qquad\qquad \overline{A + B} = \overline{A}\cdot\overline{B}
$$

Generalización a $n$ variables:

$$
\overline{A + B + C} = \overline{A}\,\overline{B}\,\overline{C} \qquad\qquad \overline{ABC} = \overline{A} + \overline{B} + \overline{C}
$$

![Equivalencias de De Morgan entre compuertas: NAND equivale a OR con entradas negadas y NOR equivale a AND con entradas negadas](./assets/de-morgan-compuertas.png)

*Figura 2.2: Equivalencias de De Morgan expresadas con compuertas.*

> **Regla práctica:** «Rompe la barra, cambia el operador».

**Verificación por tabla de verdad** (primera ley):

| $A$ | $B$ | $\overline{A\cdot B}$ | $\overline{A} + \overline{B}$ |
|:---:|:---:|:---------------------:|:-----------------------------:|
| 0   | 0   | 1                     | 1                             |
| 0   | 1   | 1                     | 1                             |
| 1   | 0   | 1                     | 1                             |
| 1   | 1   | 0                     | 0                             |

---

## 6. Minitérminos y maxitérminos

Para $n$ variables existen $2^n$ combinaciones de entrada. A cada fila de la tabla de verdad le corresponden dos expresiones:

- **Minitérmino $m_i$:** producto de todas las variables que vale **1** únicamente en la fila $i$. Variable en 1 $\Rightarrow$ aparece sin complemento; variable en 0 $\Rightarrow$ aparece complementada.
- **Maxitérmino $M_i$:** suma de todas las variables que vale **0** únicamente en la fila $i$. Variable en 0 $\Rightarrow$ sin complemento; variable en 1 $\Rightarrow$ complementada.

$$
M_i = \overline{m_i}
$$

| $i$ | $A\,B\,C$ | $m_i$                              | $M_i$                              |
|:---:|:---------:|:----------------------------------:|:----------------------------------:|
| 0   | 0 0 0     | $\overline{A}\,\overline{B}\,\overline{C}$ | $A + B + C$                |
| 1   | 0 0 1     | $\overline{A}\,\overline{B}\,C$    | $A + B + \overline{C}$             |
| 2   | 0 1 0     | $\overline{A}\,B\,\overline{C}$    | $A + \overline{B} + C$             |
| 3   | 0 1 1     | $\overline{A}\,B\,C$               | $A + \overline{B} + \overline{C}$  |
| 4   | 1 0 0     | $A\,\overline{B}\,\overline{C}$    | $\overline{A} + B + C$             |
| 5   | 1 0 1     | $A\,\overline{B}\,C$               | $\overline{A} + B + \overline{C}$  |
| 6   | 1 1 0     | $A\,B\,\overline{C}$               | $\overline{A} + \overline{B} + C$  |
| 7   | 1 1 1     | $A\,B\,C$                          | $\overline{A} + \overline{B} + \overline{C}$ |

> **Nota:** Estas son las ocho piezas posibles; cada función elige cuáles utiliza.

---

## 7. Formas canónicas

### 7.1 Suma de productos canónica (SOP): se leen los 1

Para la función de la sirena (al menos 2 sensores):

| $i$ | $A\,B\,C$ | $F$   | Minitérmino de la fila             |
|:---:|:---------:|:-----:|:----------------------------------:|
| 0   | 0 0 0     | 0     | $\overline{A}\,\overline{B}\,\overline{C}$ |
| 1   | 0 0 1     | 0     | $\overline{A}\,\overline{B}\,C$    |
| 2   | 0 1 0     | 0     | $\overline{A}\,B\,\overline{C}$    |
| **3** | **0 1 1** | **1** | $\overline{A}\,B\,C$             |
| 4   | 1 0 0     | 0     | $A\,\overline{B}\,\overline{C}$    |
| **5** | **1 0 1** | **1** | $A\,\overline{B}\,C$             |
| **6** | **1 1 0** | **1** | $A\,B\,\overline{C}$             |
| **7** | **1 1 1** | **1** | $A\,B\,C$                        |

*Regla:* por cada fila con $F = 1$ se toma su minitérmino y se unen con OR.

$$
F = \sum m(3, 5, 6, 7) = \overline{A}BC + A\overline{B}C + AB\overline{C} + ABC
$$

### 7.2 Producto de sumas canónico (POS): se leen los 0

*Regla:* por cada fila con $F = 0$ se toma su maxitérmino y se unen con AND.

$$
F = \prod M(0, 1, 2, 4) = (A+B+C)(A+B+\overline{C})(A+\overline{B}+C)(\overline{A}+B+C)
$$

### 7.3 Una función, dos descripciones

| SOP: mira los 1                                                | POS: mira los 0                                                  |
|----------------------------------------------------------------|------------------------------------------------------------------|
| «$F$ vale 1 si la entrada es la combinación 3, o la 5, o la 6, o la 7» | «$F$ vale 1 si la entrada no es la 0, y no es la 1, y no es la 2, y no es la 4» |
| $F = \Sigma m(3, 5, 6, 7)$                                     | $F = \Pi M(0, 1, 2, 4)$                                          |

> **Nota:** Entre ambas listas aparecen todas las filas (0 a 7). Los índices de $\Pi M$ son exactamente los que faltan en $\Sigma m$. La forma canónica de una función es **única** y siempre existe.

### 7.4 Criterio de elección entre SOP y POS

| Situación                         | Forma recomendada | Motivo                                  |
|-----------------------------------|:-----------------:|-----------------------------------------|
| Pocos 1 en la tabla               | SOP               | Menos términos                          |
| Pocos 0 en la tabla               | POS               | Menos términos                          |
| Solo hay compuertas NAND (7400)   | SOP               | Implementación NAND-NAND                |
| Solo hay compuertas NOR (7402)    | POS               | Implementación NOR-NOR                  |

El criterio final es el **costo**: número de compuertas, de circuitos integrados (CI) y de niveles lógicos.

---

## 8. Resolución guiada: alarma de tres sensores

**Enunciado.** Una bodega tiene tres sensores: puerta ($A$), ventana ($B$) y movimiento ($C$). Para evitar falsas alarmas, la sirena $F$ suena si **al menos dos** sensores se activan.

| $i$ | $A$ | $B$ | $C$ | $F$   |
|:---:|:---:|:---:|:---:|:-----:|
| 0   | 0   | 0   | 0   | 0     |
| 1   | 0   | 0   | 1   | 0     |
| 2   | 0   | 1   | 0   | 0     |
| 3   | 0   | 1   | 1   | **1** |
| 4   | 1   | 0   | 0   | 0     |
| 5   | 1   | 0   | 1   | **1** |
| 6   | 1   | 1   | 0   | **1** |
| 7   | 1   | 1   | 1   | **1** |

### 8.1 De la forma canónica a la simplificada

Se aprovecha la idempotencia $ABC = ABC + ABC + ABC$: un mismo término sirve para formar tres pares adyacentes.

$$
\begin{aligned}
\overline{A}BC + ABC &= BC(\overline{A} + A) = BC \\
A\overline{B}C + ABC &= AC(\overline{B} + B) = AC \\
AB\overline{C} + ABC &= AB(\overline{C} + C) = AB
\end{aligned}
$$

$$
\boxed{F = AB + AC + BC}
$$

La forma POS simplificada se obtiene de manera análoga, agrupando maxitérminos adyacentes ($M_0M_1 = A+B$, $M_0M_2 = A+C$, $M_0M_4 = B+C$):

$$
F = \prod M(0,1,2,4) = (A+B)(A+C)(B+C)
$$

*Verificación en la fila 011:* $(0+1)(0+1)(1+1) = 1$ ✓. *En la fila 100:* $(1)(1)(0+0) = 0$ ✓.

### 8.2 Costo de cada versión

| Versión       | Compuertas                                  | Circuitos integrados             |
|---------------|---------------------------------------------|:--------------------------------:|
| Canónica      | 3 NOT + 4 AND de 3 entradas + 3 OR de 2 entradas = 10 | **4 CI:** 7404 + 2 × 7411 + 7432 |
| Simplificada  | 3 AND de 2 entradas + 2 OR de 2 entradas = 5          | **2 CI:** 7408 + 7432            |

![Comparación de la implementación canónica (4 CI) y la simplificada (2 CI) de la alarma de tres sensores](./assets/costo-alarma-canonica-vs-simplificada.png)

*Figura 2.3: Costo en circuitos integrados de la alarma: forma canónica (7404, 2 × 7411 y 7432) frente a forma simplificada (7408 y 7432).*

> **Conclusión:** lo que se simplifica en papel se ahorra en hardware.

---

## 9. Simplificación algebraica

### 9.1 Procedimiento

| Paso | Técnica                    | Identidad              |
|:----:|----------------------------|:----------------------:|
| 1    | Pares adyacentes           | $XY + XY' = X$         |
| 2    | Duplicar si hace falta     | $X = X + X$            |
| 3    | Absorción                  | $X + XY = X$           |
| 4    | Absorción del complemento  | $X + X'Y = X + Y$      |
| 5    | Consenso                   | $XY + X'Z + YZ = XY + X'Z$ |

> **Limitación:** no existe un algoritmo algebraico que garantice el mínimo. Por ello, en la Semana 3 se introducen los mapas de Karnaugh.

### 9.2 Ejemplo resuelto: $F = A + \overline{A}B + A\overline{B}C$

$$
\begin{aligned}
F &= A + \overline{A}B + A\overline{B}C && \text{expresión original} \\
  &= (A + B) + A\overline{B}C         && \text{absorción del complemento: } A + \overline{A}B = A + B \\
  &= A + A\overline{B}C + B           && \text{conmutativa} \\
  &= A + B                            && \text{absorción: } A + A(\overline{B}C) = A
\end{aligned}
$$

De tres términos (5 literales) se pasa a una sola OR de 2 entradas. *Comprobación con la fila $A=0, B=0, C=1$:* original $= 0 + 0 + 0 = 0$; simplificada $= 0 + 0 = 0$ ✓.

---

## Resumen del capítulo

| Tema                        | Idea clave                                                                    |
|-----------------------------|-------------------------------------------------------------------------------|
| Circuito = expresión        | Lo que se simplifica en papel se ahorra en hardware                           |
| La tabla manda              | Dos expresiones son equivalentes si y solo si tienen la misma tabla de verdad |
| Canónica                    | Siempre existe: $\Sigma m$ (filas con 1) y $\Pi M$ (filas con 0); es única   |
| Simplificar = elegir por costo | Menos compuertas, CI y niveles; el álgebra no garantiza el mínimo          |

---

[← Anterior: Semana 1](../semana-01/soluciones.md) | [Siguiente: Ejercicios →](./ejercicios.md)
