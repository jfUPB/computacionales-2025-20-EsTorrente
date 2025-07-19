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
  
**OBSERVACIÓN:** En "PC", el número que se observa indica la operación que AÚN NO ha sido realizada, pero es la siguiente en el código. Si se encuentra en 2, al dar clic en "step", ejecutará la línea 2. NO LA 3. Además, según investigué, el 0 antes del JMP está ahí por la estructura de las instrucciones tipo C:   

> **qué se va a calcular = cálculo; acción que sigue**  

En este tipo de operación se puede omitir la primera o la última parte, pero siempre deben estar presentes por lo menos 2/3. Como no necesita almacenar ningún dato, entonces omite la primera parte... pero igual tendría que poner algún tipo de cálculo y acción, porque las otras dos partes son obligatorias. Por eso se usa un 0, para realizar un cálculo nulo y poder simplemente ejecutar la acción de salto.

```︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶ ```
___

      
5. 🌱¿Qué valor se almacena en la dirección de memoria 16? ¿Por qué crees que es ese valor?  
   >- El número 3 (el que estaba asignado a D). Al decir que M=D, estamos indicando que en la memoria se debe guardar el valor específico de ese registro. Como fue explicado en clase, se toma la posición 16 de la memoria porque ese era el valor actual de A en el momento de la ejecución del código. La lógica de por qué el programa usa el registro A es simplemente "porque sí"

6. 🌿¿Qué instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?
   - PC 0:
      >1. Fetch: Carga @1 desde la ROM
      >2. Decode: Reconoce que es una instrucción A
      >3. Execute: Guarda el valor en el registro A y avanza a la siguiente instrucción.
         
   - PC 1:
      >1. Fetch: Carga D=A desde la ROM
      >2. Decode: Reconoce que es una instrucción C
      >3. Execute: Copia el valor del registro A al registro D y avanza a la siguiente instrucción.
         
   - PC 2:
      >1. Fetch: Carga @2 desde la ROM
      >2. Decode: Reconoce que es una instrucción A
      >3. Execute: Carga el valor 2 en el registro A al registro D y avanza a la siguiente instrucción.
         
   - PC 3:
      >1. Fetch: Carga D=D+A desde la ROM
      >2. Decode: Reconoce que es una instrucción C
      >3. Execute: Carga el valor 16 en el registro A y avanza a la siguiente instrucción.
         
   - PC 4:
      >1. Fetch: Carga @16 desde la ROM
      >2. Decode: Reconoce que es una instrucción A
      >3. Execute: Copia el valor del registro A (1) al registro D y avanza a la siguiente instrucción.
         
   - PC 5:
      >1. Fetch: Carga M=D desde la ROM
      >2. Decode: Reconoce que es una instrucción C
      >3. Execute: Toma la dirección almacenada en A, guarda el valor almacenado en D en la memoria RAM de posición del valor de A, y avanza a la siguiente instrucción.
         
   - PC 6:
      >1. Fetch: Carga @7 desde la ROM
      2. Decode: Reconoce que es una instrucción A
      3. Execute: Carga el valor 7 en el registro A (prepara para el jump) y avanza a la siguiente instrucción.
         
   - PC 7:
      1. Fetch: Carga 0;JMP desde la ROM
      2. Decode: Reconoce que es una instrucción C
      3. Execute: Hace un cálculo nulo y realiza un salto incondicional a la posición de la instrucción 7.  

8. 🌻¿Qué cambios observas en el contenido de la memoria y los registros?
   >- ⭐Registro A: cambia cada vez que se usa una instrucción de tipo @. Le asigna un valor nuevo. Al presionar el botón de reset, se borran sus datos.  
   >- 🌟Registro D: solo cambia si se asigna un valor nuevo por medio de una operación =. Al presionar el botón de reset, se borran sus datos.  
   >- ✨Memoria: la memoria ROM permanece estática, mientras que la memoria RAM cambia al darle la indicación de almacenar el valor del registro D en la posición (A). Si le doy al botón de reset, la memoria RAM y ROM conserva los datos... sólo se borra si le doy clic al botón de clear.  

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

**-- 🧐🧪✍️ EXPERIMENTO --**  
```
@SCREEN
D=A
@i
M=D
(READKEYBOARD)
@KBD
D=M
@KEYPRESSED
D;JNE
@i
D=M
@SCREEN
D=D-A
@READKEYBOARD
D;JLE
@i
M=M-1
A=M
M=0
@READKEYBOARD
0;JMP

(KEYPRESSED)
@i
D=M
@KBD
D=D-A
@READKEYBOARD
D;JGE
@16
A=M
M=-1
@i
M=M+1
@READKEYBOARD
0;JMP
```
- **🌱Lo que pensé que hacía antes de leer la documentación:**  
   > No sé exactamente qué hacen @i, @KBD y @JLE... pero solamente viendo los tags, estoy asumiendo que está checkeando en loop si una tecla del teclado está siendo presionada, y cambia algo en la apariencia de la pantalla de acuerdo a esto.

- **🌿Lo que pienso que hace después de leer la documentación:**
   > 1. Almacena el valor de la pantalla (16384) en el registro A
   > 2. Copia ese valor en el registro D
   > 3. Crea una variable i y le asigna una parte de la memoria RAM, dándole también ese valor al registro A
   > 4. Almacena el valor de D (el valor de screen) en la posición M (el valor de A, dado por la variable i)
   > 5. Crea el tag READKEYBOARD, o sea que las siguientes líneas van a encargarse de detectar el input de teclado
   > 6. Según la docu, @KBD se refiere a la posición 24576 de la RAM, que está designada para el teclado. Entonces, almacena ese valor en el registro A
   > 7. Almacena en D el valor que tiene M en la posición A
   > 9. La documentación decía que JNE significa que si el out es distinto de 0, haga un jump. Según entendí, revisa el valor de D, hace el check, y si se cumple la condición... va al tag hecho en a línea anterior (@KEYPRESSED). O sea que si es distinto de 0, va directo a realizar un cambio en la pantalla.
   > 10. Vuelve a asignar a A el valor de i (16384)
   > 11. Luego reescribe el valor del registro D de acuerdo al valor almacenado en M.
   > 12. Una vez más reescribe A con el valor original de screen.
   > 13. Como D tenía el valor de M, que es el valor del registro A, que es el valor de la variable I... (aquí ya estoy medio perdida), A toma el valor de 16384... entonces la operación sería el valor de i - 16384 (?). Según lo que recuerdo de la documentación, ese era el inicio de un ciclo while.
   > 14. La aplicación vuelve a la linea donde está el tag de (READKEYBOARD) y sigue en ese loop... a menos que D = i-16384 sea > 0. En ese caso, vuelve a darle a A el valor de i.
   > 15. En la posición i de M, guarda el valor de i - 1.
   > 16. Guarda en el registro A ese valor de la operación resultante.
   > 17. Almacena en el puesto de ese resultado de la memoria RAM el valor 0.
   > 18. Hace el salto obligatorio a READKEYBOARD.
   > 19. Ahora, en la parte de KEYPRESSED, toma el valor de i en el registro A y le asigna 16384 a D.
   > 20. Le asigna el valor de 24576 al registro A.
   > 21. Vuelve a empezar un while, haciendo el mismo check de D = i - 24576.
   > 22. Si D es >= 0, regresa al check de teclado.
   > 23. Le asigna el valor 16 a A, luego hace que A = el valor almacenado en la posición 16
   > 24. Le resta al valor de esa posición el número 1.
   > 25. Vuelve a asignar i al registro A.
   > 26. Memoria posición i = i + 1
   > 27. Salto incondicional al check de teclado.
   
   Asumiendo en base a lo que vi en la documentación y el contexto, asumo que está cambiando el valor de SCREEN para pintar pixeles si hay una tecla presionada, y despintarlos si no. Asumo que 0 es pixel en blanco.

- **🌻Lo que realmente hace:**
> 1. Almacena el valor de la pantalla (16384) en el registro A  
>    ✅ Correcto.  

> 2. Copia ese valor en el registro D  
>    ✅ Correcto.  

> 3. Crea una variable i y le asigna una parte de la memoria RAM, dándole también ese valor al registro A  
>    ❌ **i no es una dirección nueva, sino una posición de la RAM donde se guardará el valor actual del "puntero" de pantalla.** No estás creando una nueva dirección, sino usando una ya existente (probablemente RAM\[15] o algo similar).  

> 4. Almacena el valor de D (el valor de screen) en la posición M (el valor de A, dado por la variable i)  
>    ✅ Correcto.  

---

### Ciclo (READKEYBOARD)

> 5. Crea el tag READKEYBOARD, o sea que las siguientes líneas van a encargarse de detectar el input de teclado  
>    ✅ Correcto.  

> 6. Según la docu, @KBD se refiere a la posición 24576 de la RAM, que está designada para el teclado. Entonces, almacena ese valor en el registro A  
>    ✅ Correcto.  

> 7. Almacena en D el valor que tiene M en la posición A  
>    ✅ Correcto.  

> 9. La documentación decía que JNE significa que si el out es distinto de 0, haga un jump. Según entendí, revisa el valor de D, hace el check, y si se cumple la condición... va al tag hecho en la línea anterior (@KEYPRESSED).  
>    ✅ Correcto. Es un salto si **se presionó alguna tecla**.  

> 10. Vuelve a asignar a A el valor de i (16384)  
>     ❌ No necesariamente 16384. **Vuelve a apuntar a la variable `i`, que contiene el valor actual del pixel que se va a borrar**.  

> 11. Luego reescribe el valor del registro D de acuerdo al valor almacenado en M.  
>     ✅ Correcto.  

> 12. Una vez más reescribe A con el valor original de screen.  
>     ❌ Aquí no se reescribe con `SCREEN`, sino que se compara con `SCREEN`. Lo que se hace es `D = i - SCREEN`.  

> 13. Como D tenía el valor de M, que es el valor del registro A, que es el valor de la variable I... (aquí ya estoy medio perdida), A toma el valor de 16384... entonces la operación sería el valor de i - 16384 (?)  
>     ✅ Correcto. Se está haciendo `D = i - SCREEN`, y si `D <= 0`, significa que ya llegamos al comienzo de la pantalla y no hay nada que borrar.  

> 14. La aplicación vuelve a la línea donde está el tag de (READKEYBOARD) y sigue en ese loop... a menos que D = i-16384 sea > 0. En ese caso, vuelve a darle a A el valor de i.  
>     ✅ Correcto.  

> 15. En la posición i de M, guarda el valor de i - 1.  
>     ✅ Correcto.  

> 16. Guarda en el registro A ese valor de la operación resultante.  
>     ✅ Correcto. (Ahora A apunta a la nueva posición del pixel a borrar.)  

> 17. Almacena en el puesto de ese resultado de la memoria RAM el valor 0.  
>     ✅ Correcto. Borrar el pixel.  

> 18. Hace el salto obligatorio a READKEYBOARD.  
>     ✅ Correcto.  

---

### Parte de (KEYPRESSED)

> 19. Ahora, en la parte de KEYPRESSED, toma el valor de i en el registro A y le asigna 16384 a D.  
>     ❌ Error pequeño. No le asigna 16384. **Lo que hace es calcular `D = i - KBD` (24576), para saber si el puntero de pantalla (`i`) ya se salió del área válida.**  

> 20. Le asigna el valor de 24576 al registro A.  
>     ✅ Correcto, ese es `@KBD`.  

> 21. Vuelve a empezar un while, haciendo el mismo check de D = i - 24576.  
>     ✅ Correcto.  

> 22. Si D es >= 0, regresa al check de teclado.  
>     ✅ Correcto. Esto evita pintar más allá del final de la pantalla.  

> 23. Le asigna el valor 16 a A, luego hace que A = el valor almacenado en la posición 16  
>     ✅ Correcto. `@16` probablemente contiene un contador de pixeles activos o algo similar (aunque no se inicializó en este fragmento).  

> 24. Le resta al valor de esa posición el número 1.  
>     ❌ No le resta. **Pone `-1` en la posición que apunta `A=M`, es decir, pinta el pixel (enciende el bit).**  

> 25. Vuelve a asignar i al registro A.  
>     ✅ Correcto.  

> 26. Memoria posición i = i + 1  
>     ✅ Correcto.  

> 27. Salto incondicional al check de teclado.  
>     ✅ Correcto.  

---

### Resumen de lo que hace el programa:

✅ Correcto:  

> Asumo que está cambiando el valor de SCREEN para pintar pixeles si hay una tecla presionada, y despintarlos si no. Asumo que 0 es pixel en blanco.  
> ✅ **Sí, el programa crea una animación que recorre la pantalla de izquierda a derecha cuando se mantiene presionada una tecla, y borra los pixeles de derecha a izquierda cuando se suelta.**  

---

* `i` = puntero que recorre la pantalla.  
* Si NO hay tecla: se borra el pixel en `i`, se reduce `i--`.  
* Si SÍ hay tecla: se pinta el pixel en `i`, se incrementa `i++`.  
* La memoria desde `SCREEN` hasta `KBD` representa todos los pixeles (8192 palabras = 512 x 256 bits / 16 bits por palabra).  

___

```︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶```
  
**OBSERVACIONES:** Los tags que se ven en el bloc de notas como (NOMBRE) y @NOMBRE, en el simulador se convierten en números. El simulador traduce automáticamente el nombre de las variables al espacio correspondiente en la RAM. Creo que los errores que tuve al asumir el funcionamiento del programa se debían principalmente a 2 factores:  
> ⭐ Mi cerebro todavía no está totalmente familiarizado con la lógica del lenguaje. Me confundí algunas veces entre la M representando la posición indicada por A y el valor almacenado en esa posición.  

> 🌟 Fatiga por la cantidad de datos con nombres abstractos. Como tengo déficit de atención, la programación se me facilita mucho más cuando las variables y funciones tienen nombres explícitos y colores que me permiten identificar rápidamente su tipo y función. Como los nombres aquí son tan genéricos, me da un poco más de dificultad :(  

```︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶ ```
___
  
1. **🌱Identifica una instrucción que use la ALU y explica qué hace.**  
   > **D=D+A** : le dice a la ALU que sume el valor del registro A al valor del registro D, y luego lo guarde en el registro D.
   
3. **🌿¿Para qué sirve el registro PC?**  
   > Indica cuál es la posición en la memoria ROM de la siguiente operación que se va a ejecutar.
   
5. **🌻¿Cuál es la diferencia entre @i y @READKEYBOARD?**  
   > @i se está refiriendo a una dirección de la RAM donde se almacenan valores (como una variable), y @READKEYBOARD se refiere a una etiqueta (un punto específico en el código).
   
7. **🌱Describe qué se necesita para leer el teclado y mostrar información en la pantalla**.  
   > Activar el teclado en el simulador con el botón de enable keyboard, y hacer uso de las etiquetas reservadas @KBD y @SCREEN.  
   > - Si el valor de M para KDB es distinto de 0, una tecla está siendo presionada.  
   > - Para escribir en la pantalla, se hace a partir de la dirección de SCREEN, donde cada posición representa 16 pixeles.
    
9. **🌿Identifica un bucle en el programa y explica su funcionamiento.**
   > la etiqueta (READKEYBOARD) es un bucle que se ejecuta constantemente.
   >1. @KBD: Carga la dirección del teclado (24576) en A
   >2. D=M: Lee el valor de la memoria en KBD (0 si no hay tecla presionada) y lo guarda en D
   >3. @KEYPRESSED: Prepara para checkeo de tecla
   >4. D;JNE: Salta a KEYPRESSED si D no es cero (si hay tecla presionada)
   >5. @i: Carga la dirección de 'i'
   >6. D=M: Obtiene el valor almacenado en 'i' (posición actual en pantalla)
   >7. @SCREEN: Carga la dirección base de la pantalla
   >8. D=D-A: Calcula cuánto hemos avanzado desde el inicio de la pantalla
   >9. @READKEYBOARD: Prepara para saltar al inicio del bucle
   >10. D;JLE: Si D <= 0 (se limpió la pantalla), vuelve al bucle
   >11. Si no hay tecla, borra un píxel (M=0 en dirección i)
   >12. Vuelve a saltar a (READKEYBOARD)
   
11. **🌻Identifica una condición en el programa y explica su funcionamiento.**
    > *D;JNE:* es una condición que hace un check del valor de D. Si es distinto a 0, salta al tag en la línea anterior.
