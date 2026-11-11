
## **Semana 2: Álgebra de Boole y Formas Canónicas**


## 📌 **1. Circuitos y Expresiones Booleanas**
Un circuito digital y una expresión algebraica son exactamente lo mismo: cada cable de entrada es una variable, las compuertas representan operaciones y la salida refleja el valor final.

<img width="290" height="195" alt="image" src="https://github.com/user-attachments/assets/39018649-4610-429b-94c1-82a1ebe86ad1" />

*Figura 2.1: Como se observa, una compuerta AND funciona como producto, la OR como suma y la NOT como complemento o negación.*

* **Precedencia de operadores:** Primero se resuelve la negación (NOT), luego el producto (AND) y al final la suma (OR).

---
## 📌 **2. Postulados y Teoremas del Álgebra de Boole**
El álgebra de Boole opera con el conjunto {0, 1} mediante las operaciones suma (+), producto y negación. No es necesario memorizar las tablas; se consultan y aplican según la necesidad.

<img width="528" height="155" alt="image" src="https://github.com/user-attachments/assets/c278a151-be07-4f4b-a3c5-41804fc959e4" />
<img width="525" height="247" alt="image" src="https://github.com/user-attachments/assets/d22ebdd0-7de7-48ea-a4a1-b2fb6dbe46b2" />

*Figura 2.1: Postulados de Huntington (identidad, complemento, conmutativa y distributiva) con su principio de dualidad, y la tabla de consulta de teoremas (absorción, adyacencia y consenso).*

---

## ⚖️ **3. Leyes de De Morgan**
Las leyes de De Morgan permiten transformar expresiones lógicas complejas cambiando de operador y distribuyendo las negaciones.

<img width="541" height="257" alt="image" src="https://github.com/user-attachments/assets/97529e0f-a060-4883-be50-a10808e7476b" />

*Figura 2.2: Equivalencias gráficas. Arriba: una compuerta NAND equivale a una OR con entradas negadas ((AB)' = A' + B'). Abajo: una compuerta NOR equivale a una AND con entradas negadas ((A + B)' = A'B'). Regla práctica: rompe la barra, cambia el operador.*

## 🧩 **4. Minitérminos y Maxitérminos (Formas Canónicas)**
A partir de una tabla de verdad, podemos representar cualquier función de dos formas estándar:

* **SOP (Suma de Minitérminos):** 
  * Se leen las filas donde la salida vale 1.
  * Se toma la variable sin negar si vale 1 y negada si vale 0, uniéndolas con producto y luego sumando los términos.
* **POS (Producto de Maxitérminos):**
  * Se leen las filas donde la salida vale 0.
  * Se niega la variable si vale 1 y se deja normal si vale 0, uniéndolas con suma y multiplicando los bloques.

---

## ⚙️ **5. Ejemplo Práctico: Alarma de Tres Sensores**
Supongamos una bodega con puerta (A), ventana (B) y movimiento (C). La alarma debe sonar si al menos dos sensores se activan.

* **Tabla canónica (SOP):** Se agrupan los minitérminos donde la función se activar.
 <img width="311" height="275" alt="image" src="https://github.com/user-attachments/assets/cdd47417-d7d1-4d37-964c-f00dd35b057f" />

* **Simplificación algebraica:** Agrupando términos mediante propiedades, la expresión gigante se reduce notablemente:
<img width="575" height="300" alt="image" src="https://github.com/user-attachments/assets/83ba2ecf-2857-4681-9294-bdbfcf876812" />

  
**F = AB + AC + BC**

<img width="712" height="283" alt="image" src="https://github.com/user-attachments/assets/f6aa1982-efe5-4983-baa9-497505ecd878" />

*Figura 2.2: Lo que simplificas en papel lo ahorras en hardware. El circuito canónico requiere múltiples chips complejos, mientras que la versión simplificada reduce drásticamente los componentes.*

---

[⬅️ Volver al Índice Principal](../README.md)
