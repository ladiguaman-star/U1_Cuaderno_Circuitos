# 📖 UNIVERSIDAD NACIONAL DE LOJA
### **Diseño de Circuitos - Unidad 1**
## **Semana 1: Sistemas Numéricos, Códigos y Compuertas Lógicas**


## 📌 **1. Representación Binaria y Márgenes de Ruido**
En los sistemas digitales no trabajamos con voltajes exactos, sino con rangos. Un transistor funciona como un interruptor, por lo que se definen umbrales de seguridad para saber cuándo el circuito lee un 1 o un 0.

<img width="652" height="338" alt="image" src="https://github.com/user-attachments/assets/0a13cc0c-ae18-4cbe-8571-726d2875da7f" />

*Figura 1.1: Como ves en la imagen, el emisor promete ciertos voltajes y el receptor exige otros. La franja del centro es la zona indefinida (entre 0,8V y 2,0V), donde el chip no sabe si lee un 0 o un 1 (suele pasar si dejas una entrada desconectada).*

* **Margen de Ruido Alto (NMH):** Es el colchón de seguridad para los niveles altos (2,7 V - 2,0 V = 0,7 V).
* **Margen de Ruido Bajo (NML):** Es el colchón para los niveles bajos (0,8 V - 0,5 V = 0,3 V).

---

## 🔢 **2. Sistemas Numéricos y Conversiones**
A diferencia de los números romanos (que no dependen de dónde estén colocados), en electrónica los sistemas son posicionales: cada posición vale una potencia de la base.

* **Binario a Decimal:** Se suman las potencias de 2 (1, 2, 4, 8, 16...). 
  * *Ejemplo:* El binario 1011 equivale a 8 + 0 + 2 + 1 = 11 en decimal.
* **Decimal a Binario:** Se divide sucesivamente entre 2 y se leen los residuos de abajo hacia arriba.
* **Hexadecimal y Octal:** Se usan como abreviaturas prácticas agrupando los bits de 4 en 4 (Hex) o de 3 en 3 (Octal).

---

## ➕ **3. Complemento a Dos (Números Negativos)**
Para representar números negativos sin utilizar el signo menos, los sistemas digitales usan el complemento a dos.

<img width="700" height="350" alt="image" src="https://github.com/user-attachments/assets/1d998399-aec0-4fb1-829d-78c9610498ec" />

*Figura 1.2: El gráfico lo explica claro: para hallar el negativo de un número (como el 3), primero se pasa a binario (0011), luego se invierten los bits (1100) y finalmente se suma 1, obteniendo 1101 que representa al -3.*

> **La gran ventaja:** Gracias a esto, el circuito no necesita un restador físico; el mismo sumador hace las restas y el bit que sobra a la izquierda simplemente se descarta.

---

## 🏷️ **4. Códigos Digitales Principales**
* **BCD (Decimal Codificado en Binario):** Cada dígito decimal se escribe usando 4 bits por separado (ej. el 157 se separa en 1, 5 y 7). Se usa muchísimo en los displays de los contadores y relojes.
* **Código Gray:** Diseñado para que al avanzar de un número al siguiente solo cambie un bit a la vez. Esto evita que los sensores o perillas (encoders) lean datos falsos durante el cambio.
* **ASCII:** Es el estándar mundial de 7 bits que traduce letras y símbolos a números para que la computadora los entienda (por ejemplo, la letra A equivale al 65).

---

## 🔌 **5. Compuertas Lógicas y el Circuito Integrado 74LS08**
Las funciones lógicas básicas (NOT, AND, OR, NAND, NOR, XOR, XNOR) vienen empaquetadas en circuitos integrados físicos para armar en el protoboard.

<img width="282" height="285" alt="image" src="https://github.com/user-attachments/assets/1b68c251-1290-487f-94b1-11c7693b349f" />

*Figura 1.3: Distribución de pines del chip 74LS08 (encapsulado DIP-14). La muesca superior guía la posición: el pin 1 está arriba a la izquierda y la numeración baja en contra del reloj.*

* **Alimentación obligatoria:** Debes conectar siempre el Pin 14 a +5V (VCC) y el Pin 7 a Tierra (GND) o el chip no encenderá ni funcionará.
* **Alternativa:** Si no hay 74LS08, puedes usar el 74HC08 (tecnología CMOS) que hace exactamente lo mismo y tiene los mismos pines.

---

[⬅️ Volver a la Portada (Índice Principal)](Portada.md)
