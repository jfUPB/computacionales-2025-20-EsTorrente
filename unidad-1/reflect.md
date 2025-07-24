# Unidad 1

## 🤔 Fase: Reflect
### 📝**Actividad 05**
🌱Parte 1: recuperación de conocimiento (retrieval practice)

**Describe con tus palabras las tres fases del ciclo Fetch-Decode-Execute. ¿Qué rol juega el Program Counter (PC) en este ciclo?**  
>🍃FETCH: el computador busca la operación que corresponde a esa etapa del ciclo dentro de la memoria ROM.  
>🍂DECODE: el computador interpreta la operación a realizar y asigna los recursos necesarios para llevarla a cabo.  
>🍁EXECUTE: el computador ejecuta la operación (sumas, almacenar datos en memoria o registros...)  
  
**¿Cuál es la diferencia fundamental entre una instrucción-A (que empieza con @) y una instrucción-C (que involucra D, M, A, etc.) en el lenguaje ensamblador de Hack? Da un ejemplo de cada una.**
>🍃INSTRUCCIONES A: asignan un valor al registro A. Permiten preparar saltos de posición para recuperar el dato almacenado en la memoria RAM[A], o simplemente indicar la posición de memoria ROM[A] a la que se quiere regresar (incluyendo tags). Con ella se pueden asignar secciones de memoria a una variable. Sólo tienen ese argumento de @valor.
>
>🍂INSTRUCCIONES B: Su estructura está compuesta por 3 partes: `almacenamiento = operación; acción`. De esas 3 partes, la primera o la tercera pueden ser obviadas, pero siempre debe permanecer 2/3 completa. Sirve para realizar checks lógicos, saltos, reescribir el registro D o modificar un valor en la memoria RAM indicada.  
  
**Explica la función de los siguientes componentes del computador Hack: el registro D, el registro A y la ALU.**  
>🍃REGISTRO A: sirve para cambiar directamente el valor del registro D, intercambiándolo por el dato almacenado. Además, es el que indica la posición a la cuál se realizan los saltos y la posición de la memoria RAM que está siendo manipulada.
>
>🍂REGISTRO D: funciona principalmente para realizar operaciones y almacenar valores numéricos (como los resultados de esas operaciones), y luego asignar esos datos a una parte de la memoria si se desea. También se utiliza para realizar saltos, checkeando la condición del valor almacenado. 
>
>🍁LA ALU: Es la parte del computador que se encarga de interpretar las operaciones matemáticas, asignar los recursos necesarios y ejecutarlos. 

**¿Cómo se implementa un salto condicional en Hack? Describe un ejemplo (p. ej., saltar si el valor de D es mayor que cero).**
> Lo primero es usar una instrucción tipo A para indicar la ubicación a la que vamos a saltar en la memoria ROM si la condición se cumple. Después, usando la estructura que mencioné para las instrucciones tipo C, podemos eliminar la segunda parte (solamente necesitamos el registro que vamos a checkear y la acción a realizar). Nos quedaría solamente `almacenamiento; acción`. La acción que queremos realizar es un salto que revise la condición que necesitamos, por lo que usamos: "JGT" `(Jump -> greater than)`, "JLE" `(Jump -> lower equal), "JGE" (Jump -> greater equal), etc. Por último, simplemente reemplazamos "almacenamiento" con el registro que tiene el valor que revisamos (usualmente D).
>
> Un ejemplo para realizar un salto a la posición 16 de la memoria ROM si el valor de D es mayor que 0:  
> `@16`  
> `D;JGT`    

**¿Cómo se implementa un loop en el computador Hack? Describe un ejemplo (p. ej., un loop que decremente un valor hasta que llegue a cero).**
> Por medio de una variable, un tag y un salto condicional. Primero, creamos la variable que va a corresponder a i (el número actual de iteraciones) para que se le asigne una posición en la memoria RAM. Cada vez que el loop termine las operaciones que le asignamos, tendremos que hacer lo siguiente:
> 1. utilizar una operación tipo A para llamar la posición de la memoria RAM de la variable i.
> 2. asignar el valor almacenado en ese espacio al registro D.
> 3. utilizar otra operación tipo A para asignarle al registro A el número total de iteraciones que queremos que se ejecuten.
> 4. realizar el cálculo D=D-A
> 5. Realizar un check que revise si el valor de D es mayor que 0. Si lo es, ya se completaron las iteraciones deseadas, y el programa puede salir del loop. Esto se hace con una operación tipo A hacia un tag / posición distinto, y "D;JGT". Si aún no se cumple, el programa se sigue ejecutando para incrementar el valor de i así:
> 6. volver a cargar a posición de memoria RAM[i]
> 7. Sumarle 1 al valor almacenado en esa memoria.
>
> Los pasos 3 y 4 son opcionales si no queremos un número específico de iteraciones. Podemos simplemente checkear si después del código dentro el loop, se cumplió que `D;JE`

**¿Cuál es la diferencia entre la instrucción D=M y la instrucción M=D?**
> 🍃D=M: está almacenando en el registro D el valor que está en la memoria RAM[A]  
> 🍂M=D: almacena en la memoria RAM[A] el valor almacenado en el registro D.  

**Describe brevemente qué se necesita para leer un valor del teclado (KBD) y para “pintar” un pixel en la pantalla (SCREEN).**  
> Lo primero es activar el uso del teclado en el simulador. Luego se utilizan los tags @KBD y @SCREEN dentro de las instrucciones para reescribir la parte de la memoria RAM asignada al teclado y la pantalla.
>    
> 🍃Si el valor almacenado en RAM[KBD] es distinto a 0, entonces hay una tecla siendo presionada.  
> 🍂En la memoria RAM[SCREEN], cada una de las 16 posiciones representa un conjunto de pixeles. Si mal no recuerdo, 0 significa que el pixel está en blanco y 1 representa que el pixel está en negro.
>   
> Usando esas indicaciones, podemos crear un salto condicional que checkee el valor en RAM[KBD], y si el valor es mayor que 0, salte a la sección que aumenta el valor en RAM[SCREEN] hasta pintar toda la pantalla.  
___
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
🌱REFLEXIÓN: **¿Cuál fue el concepto o actividad más desafiante de esta unidad para ti y por qué?**
> La de analizar el código que pintaba y despintaba la pantalla. Como mencioné en la bitácora, como los nombres de las variables son muy abstractas y tienen tantos roles distintos que pueden jugar, se me dificulta un poco identificar cuál es el papel de cada uno en cada línea de código específica... aunque siento que ya le he cogido el tiro a identificarlo.   

🌿**La metodología de “predecir, ejecutar, observar y reflexionar” fue central en nuestras actividades. ¿En qué momento esta metodología te resultó más útil para entender algo que no tenías claro?**
> En ese mismo ejercicio de la pantalla. Me pareció bueno predecir el funcionamiento antes de leer la documentación y después de leerla, porque me permitió comprobar que sí había comprendido mucho de lo que leí. También fue muy útil sentarme a analizar los errores en el código y buscar el motivo por el cuál me estaba equivocando, más allá de simplemente decir que algo falló.

🌼**Describe un momento “¡Aha!” que hayas tenido durante estas dos semanas. ¿Qué estabas haciendo cuando ocurrió?**
> Durante el último ejercicio de la fase apply (sumar los números del 1 al 5), había escrito "D=M+D" o algo así. Cuando fui a cargar el programa, todo salía vacío en la memoria ROM. Tuve que borrar línea por línea y volverlo a cargar para identificar lo que estaba provocando el conflicto. Como 5 minutos después fue que descubrí (a las malas) que la D debe ir primero en las operaciones. Después de corregirlo a "D=D+M", todo funcionó.

🌻**Pensando en la próxima unidad, ¿Qué harás diferente en tu proceso de estudio para aprender de manera más efectiva?**  
> Quizás responder las preguntas de teoría a medida que se explican en la clase. Considero que todo lo demás en mi método fue bastante efectivo.  
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
___
