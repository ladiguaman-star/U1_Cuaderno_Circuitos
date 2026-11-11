
## **Semana 4: Circuitos Aritméticos (Sumadores, Restadores y Comparadores)**

## 📌 **1. Suma de un Solo Bit y Tipos de Sumadores**
Para sumar números binarios, operamos columna por columna igual que en el sistema decimal: se escribe un resultado ($S$) y se genera un acarreo (*carry* o $C$ que "me llevo"). Dependiendo de la posición, se usan dos tipos de circuitos:

* **Semisumador (*Half Adder*):** Suma únicamente dos bits (A y B). Como no recibe un acarreo previo, solo sirve para la **columna 0** (la más a la derecha).
  * *Ecuaciones:* S = A ⊕ B y  C = A ⊕ B.
* **Sumador Completo (*Full Adder*):** Suma tres bits: A, B y el acarreo de entrada (C_in) que viene de la columna anterior.
  * *Regla práctica:* La salida $S = 1$ cuando hay un número **impar de unos** (1 o 3), y el acarreo de salida (C_out = 1) cuando hay **al menos dos unos**.

<img width="680" height="200" alt="image" src="https://github.com/user-attachments/assets/9c2f34ac-06d9-485a-9d8a-a0db72847d3a" />


*Figura 4.1: Conexión en cascada de cuatro sumadores completos para operar con 4 bits. El acarreo de salida (C_out) de un sumador se convierte en el acarreo de entrada (C_in) del siguiente.*

---

## 🌊 **2. Sumador de 4 Bits y el Retardo (*Ripple Carry*)**
Cuando conectamos varios sumadores completos en cadena, el acarreo debe propagarse de derecha a izquierda etapa por etapa.


* **Efecto Ola (*Ripple*):** Cada sumador debe esperar a que el sumador anterior calcule y entregue su acarreo. Por esta razón, el resultado completo tarda un poco más en estabilizarse.
  <img width="627" height="157" alt="image" src="https://github.com/user-attachments/assets/509b097b-3105-4677-8e98-31304fcdb293" />

* **Estimación del retardo:** Si cada compuerta tarda aproximadamente $10\text{ ns}$ y el acarreo cruza dos compuertas por etapa, un sumador de 4 bits tomará alrededor de $80\text{ ns}$, y uno de 16 bits unos $320\text{ ns}$ (a mayor cantidad de bits, mayor retardo).

---

## ➖ **3. La Resta Mediante el Sumador (Inversor Controlado)**
En los circuitos digitales no se diseña un restador físico independiente; en su lugar, **restar es sumar el número negativo** usando el complemento a dos:
$$A - B = A + (-B)$$

* Para convertir el sumador en restador, se añade una línea de control $M$ conectada a compuertas XOR en cada bit de B:
  * Si $M = 0$: $B$ pasa igual $\rightarrow$ el circuito **suma**
  * Si $M = 1$: $B$ se invierte (se niegan sus bits) y el $C_{in}$ inicial se pone en $1$, lo que equivale automáticamente a sumar $1$ (complemento a dos) $\rightarrow$ el circuito **resta**.

---

## ⚠️ **4. Desbordamiento (*Overflow*)**
Cuando operamos con números con signo de 4 bits (rango de $-8$ a $+7$), puede ocurrir que el resultado de la operación sea demasiado grande para caber en 4 bits.

* **Dato clave:** El $C_{out}$ final **no** indica necesariamente un error.
* **Cómo se detecta el Overflow ($V$):** Ocurre cuando el acarreo que entra a la última etapa es diferente al acarreo que sale de ella:
  V = C_3  ⊕ C_4

---

## 📐 **5. Comparador de Magnitud**
Es un circuito combinacional que evalúa dos números binarios para determinar si son iguales ($A = B$) o si uno es mayor que otro ($A > B$).
* Utiliza compuertas XNOR bit a bit para verificar la igualdad y analiza desde el bit más significativo (izquierda) para determinar qué número es mayor. En los laboratorios se suele emplear el circuito integrado comercial **7485**.

---

[⬅️ Volver a la Portada (Índice Principal)](README.md)
