# Unidad 1

## 🔎 Fase: Set + Seek

### **Actividad 01**

El propósito de esta actividad es entender cómo funciona el ciclo fetch-decode-execute. 
  
1. 🌱 **¿Qué es el fetch?**
    >- El computador busca la instrucción correspondiente en el programa cargado.
      
3. 🌿 **¿Qué es el decode?**
    >- El computador interpreta la instrucción correspondiente y asigna recursos para ejecutarla.
      
4. 🌻 **¿Qué es el execute?**
    >- El computador realiza la operación.

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
   - **🌱Lo que pensé que hacía:**  
     >realiza una suma entre los datos almacenados en A y D, pero no asigna nada a M porque no hay una variable con ese nombre.
       
   - **🌿Lo que realmente hace:**
      >1. Almacena el #1 en A
      >2. Almacena el valor de A en D
      >3. Almacena el #2 en A
      >4. Suma A y D, y lo almacena en D
      >5. Almacena el #16 en A
      >6. Guarda en la memoria RAM el valor de D, en la posición del valor de A
      >7. Almacena el #7 en A
      >8. Hace un computo nulo, y después salta a la instrucción del valor de A
___

```︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶```
  
**OBSERVACIÓN:** En "PC", el número que se observa indica la operación que AÚN NO ha sido realizada, pero es la siguiente en el código. Si se encuentra en 2, al dar clic en "step", ejecutará la línea 2. NO LA 3.

```︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶ ```
___

      
5. 🌱¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor?  
   >- El número 3 (el que estaba asignado a D). Al decir que M=D, estamos indicando que en la memoria se debe guardar el valor específico de ese registro. Como fue explicado en clase, se toma la posición 16 de la memoria porque ese era el valor actual de A en el momento de la ejecución del código. La lógica de ese proceso es simplemente "porque sí"

6. 🌿¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?
   >- nxoinoisaxasx

8. 🌻¿Qué cambios observas en el contenido de la memoria y los registros?
   >- ⭐Registro A: cambia cada vez que se usa una instrucción de tipo @. Le asigna un valor nuevo.  
   >- 🌟Registro D: solo cambia si se asigna un valor nuevo por medio de una operación =.  
   >- ✨Memoria: la memoria ROM permanece estática, mientras que la memoria RAM cambia al darle la indicación de almacenar el valor del registro D en la posición (A).   

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
  
8. **🌱¿Qué diferencia hay entre los datos almancenados en la memoria ROM y en la RAM?**
   >- ⭐La memoria ROM almacena el programa a ejecutar, es solamente de lectura.  
   >- 🌟La memoria RAM almacena datos temporales en una posición indicada.

___

### **Actividad 02**

1. Identifica una instrucción que use la ALU y explica qué hace.
2. ¿Para qué sirve el registro PC?
3. ¿Cuál es la diferencia entre @i y @READKEYBOARD?
4. Describe qué se necesita para leer el teclado y mostrar información en la pantalla.
5. Identifica un bucle en el programa y explica su funcionamiento.
6. Identifica una condición en el programa y explica su funcionamiento.
