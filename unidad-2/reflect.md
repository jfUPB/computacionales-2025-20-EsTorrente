# Unidad 2


## 🤔 Fase: Reflect  
### 📝Actividad 07   

🌱Explica cómo se representa y manipula un puntero en el lenguaje ensamblador de Hack. Describe las operaciones equivalentes a p = &a (asignar dirección) y *p = 20 (escribir a través del puntero) usando instrucciones de ensamblador.  
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
  
🌿¿Cómo implementarías el acceso a un elemento de un arreglo, como arr[j], en lenguaje ensamblador? Describe el rol de la dirección base del arreglo y el índice j en esta operación. 
> El rol de la dirección base del arreglo es denotar el punto de la memoria RAM donde este empieza. El índice `j` indica la posición dentro del arreglo donde se encuentra el valor que buscamos. Para implementarlo en en ensamblador, haría uso de un puntero cuya única función sea dirigir al registro A a la ubicación que le corresonde al arr[j].  
  
🌼¿Cuál fue el concepto más abstracto o difícil de “traducir” de C++ a ensamblador en esta unidad (punteros, ciclos, arreglos)? ¿Qué hiciste para lograr entenderlo?  
> Los ciclos, arreglos y punteros se sintieron bastante sencillos de introducir. Quizás en poca medida los ciclos fueron un tris más complejos, debido a que hay que prestar mucha atención al valor inicial de i, a las condiciones de salto y el orden de las instrucciones... pero todo es bastante intuitivo después de un poco de práctica.  
  
🌻En la Actividad 06 se sugirió construir el programa “PASO A PASO mediante pruebas”. ¿Cómo te ayudó este enfoque a manejar la complejidad del problema?  
> Me ayudó bastante. Definitivamente ayuda demasiado el método de empezar por el final y a grandes rasgos, simplemente dejando anotaciones de lo que debo hacer en cada uno de los ciclos, e irlo llenando poco a poco. Siento que en un programa como ese puede volverse demasiado abrumador intentar programar de corrido desde el inicio. Además, las pruebas de por medio permitían identificar errores fácilmante antes de que el código tomara más complejidad, permitiendo corregirlos sin el sufrimiento de ir línea por línea buscando qué anda mal.  
  
🌱Esta unidad fue el “puente” hacia C++. ¿Qué concepto de bajo nivel te sientes más seguro de poder identificar cuando lo veas implementado en C++?  
> En general siento que todo fue bastante sencillo... pero creo que podría hacer la coneción fácilmente entre la manera en la que los ciclos funcionan en assembly y lo que cada una de esas acciones representa de manera más compacta en C++.   
