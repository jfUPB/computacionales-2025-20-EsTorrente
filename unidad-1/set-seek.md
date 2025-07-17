# Unidad 1

## 🔎 Fase: Set + Seek

### **Actividad 01**

El propósito de esta actividad es entender cómo funciona el ciclo fetch-decode-execute. 
  
1. ¿Qué es el fetch?
    - El computador busca la instrucción correspondiente.
      
3. ¿Qué es el decode?
    - El computador interpreta la instrucción asignada.
      
4. ¿Qué es el execute?
    - El computador ejecuta esa instrucción.

___

``` asm
@1
D=A
@2
D=D+A
@16
M=D
@7
0;JMP
```
  
4. **¿Qué crees que haga este programa?**
   - **Lo que pensé que hacía:** realiza una suma entre los datos almacenados en A y D, pero no asigna nada a M porque no hay una variable con ese nombre.
       
   - **Lo que realmente hace:**
      1. Almacena el #1 en A
      2. Almacena el valor de A en D
      3. Almacena el #2 en A
      4. Suma A y D, y lo almacena en D
      5. Almacena el #16 en A
      6. Guarda en la memoria el valor de D, en la posición del valor de A
      7. Almacena el #7 en A
      8. Hace un computo nulo, y después salta a la instrucción del valor de A

**OBSERVACIÓN:** En "PC", el número que se observa indica la operación que AÚN NO ha sido realizada, pero es la siguiente en el código. Si se encuentra en 2, al dar clic en "step", ejecutará la línea 2. NO LA 3.

___

### **-- 🧐🧪✍️ EXPERIMENTO --**

Escribe un programa en lenguaje ensablador que sume los números 5 y 10, y almacene el resultado en la dirección de memoria 20. Utiliza el simulador de la CPU Hack para ejecutar tu programa y verifica que el resultado es correcto.

``` asm2
@5
D=A
@10
D=D+A
@20
M=D
```
  
5. **¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?**
   - La memoria ROM almacena la información de las operaciones a realizar. La memoria RAM contiene datos específicos en que decidimos almacenar en una posición indicada.
