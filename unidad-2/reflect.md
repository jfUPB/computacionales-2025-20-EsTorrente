# Unidad 2


## 🤔 Fase: Reflect  
### 📝Actividad 07   

🌱 **Explica cómo se representa y manipula un puntero en el lenguaje ensamblador de Hack. Describe las operaciones equivalentes a `p = &a` (asignar dirección) y `*p = 20` (escribir a través del puntero) usando instrucciones de ensamblador.**
> Un puntero puede ser cualquier variable o posición de la memoria RAM[] designado únicamente para apuntar a la dirección una variable o reescribirla. Para asignarle una dirección:
```program.asm
  @a //cargamos la posición de la variable a almacenar
  D=A //se la asignamos a D
  @p //cargamos el puntero
  M=D //almacenamos la posición (que guarda D) en la memoria que le corresponde a @p.
```
> por otro lado, para reescribir el valor de una variable por medio de un puntero:
```program.asm
  @20 //cargamos el valor a almacenar
  D=A //lo almacenamos en D
  @p //cargamos la posición que está almacenada en p (el lugar de la memoria RAM donde está el número que vamos a modificar)
  A=M //le indicamos al programa que esa posición almacenada es el nuevo lugar de la memoria a la que debe dirigirse
  M=D //le asignamos el valor de D a RAM[a]
```
  
🌿 **¿Cómo implementarías el acceso a un elemento de un arreglo, como arr[j], en lenguaje ensamblador? Describe el rol de la dirección base del arreglo y el índice j en esta operación.** 
> El rol de la dirección base del arreglo es denotar el punto de la memoria RAM donde este empieza. El índice `j` indica la posición dentro del arreglo donde se encuentra el valor que buscamos. Para implementarlo en en ensamblador, haría uso de un puntero cuya única función sea dirigir al registro A a la ubicación que le corresonde al arr[j].  
  
🌼 **¿Cuál fue el concepto más abstracto o difícil de “traducir” de C++ a ensamblador en esta unidad (punteros, ciclos, arreglos)? ¿Qué hiciste para lograr entenderlo?**  
> Los ciclos, arreglos y punteros se sintieron bastante sencillos de introducir. Quizás en poca medida los ciclos fueron un tris más complejos, debido a que hay que prestar mucha atención al valor inicial de i, a las condiciones de salto y el orden de las instrucciones... pero todo es bastante intuitivo después de un poco de práctica.  
  
🌻 **En la Actividad 06 se sugirió construir el programa “PASO A PASO mediante pruebas”. ¿Cómo te ayudó este enfoque a manejar la complejidad del problema?**  
> Me ayudó bastante. Definitivamente ayuda demasiado el método de empezar por el final y a grandes rasgos, simplemente dejando anotaciones de lo que debo hacer en cada uno de los ciclos, e irlo llenando poco a poco. Siento que en un programa como ese puede volverse demasiado abrumador intentar programar de corrido desde el inicio. Además, las pruebas de por medio permitían identificar errores fácilmante antes de que el código tomara más complejidad, permitiendo corregirlos sin el sufrimiento de ir línea por línea buscando qué anda mal.  
  
🌱 **Esta unidad fue el “puente” hacia C++. ¿Qué concepto de bajo nivel te sientes más seguro de poder identificar cuando lo veas implementado en C++?**  
> En general siento que todo fue bastante sencillo... pero creo que podría hacer la coneción fácilmente entre la manera en la que los ciclos funcionan en assembly y lo que cada una de esas acciones representa de manera más compacta en C++.

___
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
### 📝Actividad 08

[Bitácora de mi compañero](https://github.com/jfUPB/computacionales-2025-20-Valencia33/blob/unidad2/apply/unidad-2/apply.md)     

```program.asm
(LLENAR)
@4 // Posición memoria contador para llenar el array
M=M+1 
D=M // 1er valor del 1er puesto
@15
A=D+A // Salta al valor 16, 17, 18... etc. depende de D
M=D
@10 // Cambiar hasta el punto que se requiera llenar el array.
D=D-A
@LLENAR
D;JNE
@FOR
0;JMP

(FOR)
@5 // Posición memoria contador
M=M+1 
D=M // Guarda el contador en D
@15
A=D+A // A le suma el contador para coger la posición de memoria 16.
D=M // Le asigna lo que haya ahí, es decir arr[0]
@FIN
D;JEQ // Necesita que pare cuando M=0
@6 // Posición memoria suma
M=D+M // hace sum += arr[j]
@FOR
0;JMP

(FIN)
@FIN
0;JMP
```
**🌱PRUEBAS QUE VOY A REALIZAR:**
| :) | PRUEBA | PREDICT | PASÓ? | FUNCIONA? |
|----|-------|----------|-------|-----------|
| 🍃 | Ejecutar paso a paso el programa solamente hasta la parte donde el array se llene completamente, verificando que el valor asignado sea el correcto en la posición especificada y que salga del loop una vez termine. | No se está indicando el valor inicial del contador. Asumo que no habría problema si el programa se ejecuta una vez, pero si lo vuelvo a correr dándole solo a "reset" sin borrar la memoria, todo el programa se rompe. El método donde la posición del array se define en base a D también se buggeará al ejecutarlo otra vez. | Efectivamente, eso fue lo que sucedió. En la primera ejecución funcionó perfecto, pero en la segunda se rompió el programa. La solución es simplemente inicializar el contador en 0. | ✅🫴🫳
| 🍂 | Ejecutar el programa paso a paso, pero esta vez deteniéndome en cada una de las operaciones para confirmar que sí se esté agregando correctamente al espacio de memoria donde almacene @suma y verificar que el resultado se correcto. | Debido al mismo problema que mencioné anteriormente, asumo que la suma funcionará perfectamente en la primera ejecución... pero en la segunda, nunca va a llegar a la suma y el valor de la memoria no cambiará en absoluto, porque jamás pasará el check de @LLENAR -> D;JNE. | Sí, pasó exactamente eso. Igualmente, la suma se realizó correctamente :> | ✅
| 🍁 | Dejar correr al programa en su totalidad, asegurándome de que el loop del final sí detenga el programa correctamente. | Como ya mencioné, el programa va a correr perfectamente en la primera vez. | Sí, funcionó en la primera prueba y se detuvo correctamente en el loop (FIN). | ✅

___
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
### 📝Actividad 09  
  
🌱 **Continuar: ¿Qué actividad, problema o explicación de esta unidad te ayudó más a entender la conexión entre el bajo y el alto nivel? ¿Qué debería mantener sin cambios?**  
> Me gustó mucho ir comparando los ciclos en c++ y ensamblador. Siento que me ayudó a dejar de ver las funciones simplemente como un grupito de palabras que al juntarlas hacen operaciones de manera misteriosa, dejándome ver realmente qué es lo que está haciendo el computador detrás de escenas y qué rol juega cada variable.    
  
🌿**Dejar de hacer: ¿Hubo alguna actividad o concepto que te pareció redundante, demasiado confuso o que aportó poco valor a tu aprendizaje? ¿Qué eliminarías o modificarías?**  
> No, la verdad siento que todos los ejercicios sirvieron un propósito claro. Además, considero que ningún ejercicio va a estar de sobra jamás porque, en mi experiencia personal, la compresión de estos temas mejora mucho por medio de la repetición.  
  
🌼**Empezar a hacer: ¿Qué idea tienes para mejorar la próxima unidad? ¿Hay algún tipo de recurso que te habría ayudado a entender mejor los punteros o los arreglos?**  
> No, siento que todo estuvo bastante claro. Los dibujitos en la pantalla durante la explicación de los punteros fueron muy útiles para mí porque soy una persona muy visual. También fue chévere la comparación del & con un gato. Ya no lo veo igual. Quizás para una persona que se enrede más con los ejercicios de programación habría sido bueno un ejemplo más "de la manito" en clase para llenar los arreglos en ensamblador, aunque me parece que el ejercicio de llenar los pixeles de la pantalla era casi el mismo concepto.  
  
🌻**Ritmo y Dificultad: en una escala del 1 (muy fácil/lento) al 5 (muy difícil/rápido), ¿Cómo calificarías el salto de dificultad de la Unidad 1 a la Unidad 2? ¿El ritmo fue adecuado? Justifica tu calificación.** 
> 5. Me pareció bastante bueno. Considero que la unidad 1 nos dió unas bases bastante sólidas para esta nueva unidad... hasta se sintió un poco más fácil que la primera. Creo que la parte de leer la documentación fue especialmente útil como preparación.  
  
🌱**Comentario Adicional: ¿Alguna otra cosa que quieras compartir sobre cómo te sentiste aprendiendo estos conceptos?**  
> Muy cómoda. Me parece divertido... es como resolver jueguitos de puzzle. Me parece muy interesante comprender cómo funcionan los programas a los que estábamos acostumbrados en un lenguaje de programación más primitivo.
