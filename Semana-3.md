
## **Semana 3: Mapas de Karnaugh (K-Maps)**



## 📌 **1. ¿Qué es un Mapa de Karnaugh?**
El álgebra de Boole puede volverse muy compleja o depender de la pericia matemática para encontrar el mínimo. El **Mapa de Karnaugh** es una representación gráfica basada en una tabla de verdad reorganizada en una cuadrícula rectangular.

<img width="468" height="290" alt="image" src="https://github.com/user-attachments/assets/52794c74-9dbd-4967-b87c-834c3b652610" />


> **La regla de oro del K-Map:** Las celdas adyacentes (vecinas) solo deben diferenciarse en **un solo bit** gracias al uso del **código Gray** en sus filas y columnas. Esto permite aplicar visualmente la ley de adyacencia del álgebra de Boole.

---

## 🗺️ **2. Estructura de los Mapas de Karnaugh**

### **Mapa de 3 Variables (A, B, C)**
Consta de 8 celdas. Las filas representan la variable A y las columnas las variables B y C ordenadas en código Gray (00, 01, 11, 10).

<img width="287" height="172" alt="image" src="https://github.com/user-attachments/assets/6a5dd6e8-5ecc-47d5-8c3b-286dec9989f8" />

*Figura 3.1: Estructura de celdas y distribución de minitérminos (m0 a m7) en un mapa de 3 variables.*

### **Mapa de 4 Variables (A, B, C, D)**
Consta de 16 celdas. Las filas utilizan AB y las columnas CD siguiendo también el código Gray para garantizar que los vecinos solo cambien en un bit.

<img width="275" height="252" alt="image" src="https://github.com/user-attachments/assets/7bc52b8d-896c-4fa5-87ce-b41fbd251400" />

*Figura 3.2: Estructura de un mapa de 4 variables, incluyendo la vecindad toroidal (las esquinas y extremos se conectan entre sí).*

---
## ✍️ **3. Las Formas de Agrupar: ¿Cómo se debe hacer?**
Para simplificar correctamente, debes seguir estas formas y reglas visuales al armar los grupos:

* **Regla 1: Potencias de 2:** Los grupos de unos (`1`) solo pueden tener tamaños de $1, 2, 4, 8$ o $16$ celdas.
* **Regla 2: Grupos máximos:** Haz los grupos lo más grandes que puedas. Un grupo de 4 es mejor que dos de 2.
* **Regla 3: Vecindad toroidal (Los extremos se conectan):** El mapa actúa como un cilindro o esfera. Las celdas de los extremos izquierdo y derecho se conectan entre sí, al igual que las de arriba y abajo, y las cuatro esquinas se pueden unir.

<img width="647" height="162" alt="image" src="https://github.com/user-attachments/assets/cfe0af89-7674-4d14-851a-d0c9b0a2e6d4" />
<img width="647" height="162" alt="image" src="https://github.com/user-attachments/assets/61474426-1012-4a3a-9f96-216281038640" />
<img width="272" height="247" alt="image" src="https://github.com/user-attachments/assets/f3c83338-6154-4644-847c-beeb7c5e6465" />






*Figura 3.3: Ejemplos visuales de agrupamientos válidos (en bloque, en tira y conectando esquinas o extremos).*

---

## ⚙️ **4. Ejemplo Práctico Paso a Paso**
Tomemos la función de la alarma: 
$$F = \Sigma m(3, 5, 6, 7)$$

<img width="382" height="347" alt="image" src="https://github.com/user-attachments/assets/94bb9311-3d34-4ec2-a552-7fa9169b5f77" />


1. **Paso 1:** Llenamos el mapa ubicando los `1` en las celdas 3, 5, 6 y 7.
   
<img width="271" height="401" alt="image" src="https://github.com/user-attachments/assets/6c5cff55-8f96-42ae-96aa-55c67016960a" />

2. **Paso 2:** Aplicamos las formas de agrupación formando parejas o cuartetos de unos adyacentes.
   
<img width="247" height="372" alt="image" src="https://github.com/user-attachments/assets/2ec59397-a3cc-49b2-92dc-84790e2a60b2" />


3. **Paso 3:** Leemos qué variables no cambian de estado en cada grupo para obtener la ecuación final simplificada:

<img width="190" height="62" alt="image" src="https://github.com/user-attachments/assets/d821d1dd-9a63-49e8-9adf-9105ea286c08" />

---


## 🔄 **5. Condiciones «Da Igual» (Don't Care / X)**
En muchos problemas de diseño real, hay combinaciones de entrada que **nunca van a ocurrir** o cuyo resultado de salida no importa para el funcionamiento del sistema.

* Se representan con una **$X$** (o $d$) en la tabla de verdad y en el mapa de Karnaugh.
* **La gran ventaja:** Al simplificar, puedes tratar a la $X$ como un `1` si te conviene para armar un grupo más grande (de 4, 8 u 16 celdas), o como un `0` si prefieres ignorarla.
* *Regla clave:* No estás obligado a cubrirlas todas; solo usa las $X$ que realmente te ayuden a obtener una expresión más corta.

### **Ejemplo práctico de Don't Care:**
Imagina que diseñamos un circuito que solo debe activarse con los números binarios del `0` al `5` (en una aplicación de 3 bits), pero las combinaciones `6` y `7` son estados imposibles que nunca sucederán.

1. **Planteamiento:** 
   * Función original: $F = \Sigma m(1, 3, 7) + d(6)$ (donde el $7$ está en los unos y el $6$ es una condición *da igual*).
2. **En el Mapa de Karnaugh:**
   * Colocamos los `1` en las celdas 1, 3 y 7.
   * Colocamos una $X$ en la celda 6.
     
     <img width="265" height="395" alt="image" src="https://github.com/user-attachments/assets/557495f5-e1c1-40f2-851b-a77193debd64" />

3. **Estrategia de agrupación:**
   * En lugar de hacer un grupo pequeño con los unos solitarios, **usamos la $X$ de la celda 6 como si fuera un `1`** para armar un cuarteto de 4 celdas junto con el 3 y el 7.
   * Gracias a esa $X$, la expresión final se simplifica muchísimo más de lo que habría costado sin ella.


---

## ⚙️ **6. Resumen y Consejos Clave para el K-Map**
Para asegurar una simplificación perfecta en tus prácticas o exámenes:
1. **Prioriza el tamaño:** Un grupo de 8 elimina 3 variables; un grupo de 4 elimina 2; un grupo de 2 elimina 1. ¡Haz los grupos más grandes posibles!
2. **Cubre todos los 1:** Asegúrate de que cada `1` al menos pertenezca a un grupo (aunque pueden repetirse en varios grupos para solaparse).
3. **Menos grupos es mejor:** Trata de usar la menor cantidad de grupos que cubran todos los unos.

---

[⬅️ Volver a la Portada (Índice Principal)](Portada.md)


