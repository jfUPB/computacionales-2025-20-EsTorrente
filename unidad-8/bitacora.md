# Bitácora de aprendizaje de la unidad 8

## 📝 Actividad 01

🌱 **Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto?**  
> Cuando doy clic en la pantalla, el programa se congela como por 4 segundos antes de realizar el cambio de tamaño. Viendo el código, uno esperaría que simplemente se realice el cambio visual de inmediato... pero, según lo que tú nos explicaste en la clase, el cálculo que el programa realiza es TAN pesado que detiene completamente cualquier otro hilo hasta que este se haya terminado (incluyendo la capacidad de cerrar la ventana).  
  
🌿 **Ejecuta el programa y haz clic en la ventana. Observa lo que sucede. ¿Qué es lo que ves? ¿Qué es lo que esperabas ver? ¿Por qué crees que sucede esto? Observa que el programa ahora no se congela, pero el círculo no cambia de tamaño inmediatamente. ¿Por qué crees que sucede esto? ¿Qué es lo que está pasando?**  
> No encuentro `startThread();` en ninguna otra parte del código, excepto cuando se llama... entonces asumo que es parte de la biblioteca que importamos. Mi guess es que ahí llamaría lo que sea que esté dentro del método `threadedFunction()`, en este caso, el cálculo del nuevo tamaño del círculo. Como en el draw no se está llamando en ningún momento ese método para los cálculos, entonces creo que se puede seguir ejecutando sin problema. Creo que no cambia de tamaño de inmediato, pero sigue moviéndose, por lo que mencioné del draw... mientras que `heavyComputation()` sí se congela hasta terminar el cálculo, y luego realiza el cambio.

🌼 **En tus propias palabras, explica la diferencia entre concurrencia y paralelismo. ¿Por qué es importante entender esta diferencia al trabajar con hilos?**  
> `Concurrencia:` hace un poquito de muchas tareas a la vez, tan rápido que parece que las hiciera al mismo tiempo.  
> `Paralelismo:` múltiples tareas se ejecutan realmente al mismo tiempo en diferentes núcleos de la CPU.  
> Es importante entender esta diferencia porque en base al tipo que utilicemos y los specs de nuestro PC, hay que diseñar flujos diferentes de hilos en el programa.
  
___

## 📝 Actividad 02

🌻 **Analiza de nuevo el código de la actividad anterior. ¿En qué partes del código se está protegiendo el acceso a la variable circleSize? Según lo que te he venido comentando, los hilos te permiten ejecutar tareas en paralelo; sin embargo, piensa qué ocurre con el paralelismo cuando se sincroniza el acceso a un recurso compartido. ¿Qué ocurre con el rendimiento del programa? ¿Es posible que el rendimiento se vea afectado por el uso de mutex? ¿Por qué?**
> creo que se está protegiendo aquí:
```
ofSeedRandom();
circleSize = ofRandom(20, 70);
unlock();
```
> me imagino que sí se ve un poquito afectado, porque el programa debe esperar a que cada uno de los hilos entre, lo modifique y lo desbloquee... en lugar de todos hacerlo todos a la misma vez (a pesar de los posibles errores). Sin embargo, creo que en un programa como este, la diferencia debe ser como de un segundito nada más. Creo que eso se llamaba cuello de botella.  
  
🌱 **Ejecuta el código y observa el resultado. ¿Qué ocurre si cambias el valor de la variable useLock? ¿Por qué crees que ocurre esto?**
> Según recuerdo de lo explicado en clase, esto sucede porque los threads están mirando el dato del contador al mismo tiempo y realizando el cambio sobre ese valor que ven, lo que hace que los cálculos no sean correctos. Al usar el lock, un thread entra, ve el dato, modifica el contador, sale, otro entra, ve ese dato modificado, modifica el contador, sale, etc... por lo que se demora un poco más el cálculo (súper imperceptible), pero se asegura de que cada thread vea la cantidad correcta y pueda hacer sus cálculos sin error.  

🌿 **Explica en tus propias palabras ¿Cómo puede presentarse la condición de carrera en este caso? ¿Qué es lo que está pasando? Te pido que propongas un ejemplo.**
> El error en este caso es que, cuando no se usa el lock, los 4 threads están ejecutando al mismo tiempo su `threadedFunction()` e intentando hacer la operación (incrementar el contador compartido por 1). Como todos están viendo un valor distinto en el que empieza el contador, entonces sobreescriben unos sobre los cálculos de los otros... y se termina haciendo más o menos sólo 1/4 de las sumas que deberían. Si yo tengo 2 hilos que deben incrementar el contador en 1, y ambos llaman el mismo método al mismo tiempo, sin esperar a que uno haga el cálculo y le de luz verde al otro... entonces pasaría algo así:
`Contador = 0`  
AL MISMO TIEMPO:  
`Hilo 1 lee dato: contador == 0`  
`Hilo 2 lee dato: contador == 0`  
`Hilo 1 reescribe: contador = 1`  
`Hilo 2 reescribe (al mismo tiempo): contador = 1`
`Contador == 1`, en lugar del 2 que debería ser.

___

## 📝 Actividad 03

🌼 **Ejecuta el código y observa el resultado.**
> En ambos se ejecutó con mucha velocidad... pero en la versión secuencial tuve un mini drop de frames de 60 a 55 por un segundo. En el paralelo, se mantuvo en 60 (menos por un milisegundo tan irrelevante que ni alcancé a ver a cuál número droppeó).
  
🌻 **Analiza el código y estudia detenidamente su funcionamiento. En la fase de aplicación tendrás que retomar este código para resolver un reto.**
> 1. En `threadedFunction()`, está recorriendo cada pixel desde el 0 hasta la extensión de la ventana y haciendo los cálculos necesarios, para luego asignarle el color. El número está siendo mapeado con el número de iteraciones realizadas y la cantidad máxima de iteraciones.
> 2. En el setup, estamos definiendo el número máximo de iteraciones (lo que mencionaste que cambiaba el nivel de detalle del fractal) y definiendo la cantidad de pixeles en base al tamaño de la ventana.
> 3. En el draw, simplemente tenemos texto para debug donde nos dice la info de los fps, de iteraciones y esas cosas.
> 4. Al presionar espacio, se suma 1 al número de iteraciones máximas y se empieza el cálculo.
> 5. Si se presiona n, el número de iteraciones máximas se resettea a 0.
> 6. Si presiono n y luego spammeo espacio, puedo ver como en cada iteración aumenta el detalle (tal como fue descrito).
> 7. No veo ningún lock en el programa.    

🌱 **¿Qué ocurre si cambias el número de hilos?**
> Estaba usando 12. Lo cambié a 2. Mi guess es que se va a demorar más. Al ejecutarlo con los 12 hilos, se demoró `0.034 s`, mientras que con 2 se demoró `0.096 s`. La diferencia es imperceptible para mí, pero OBVIO se demoró mucho más en completar los cálculos. Me imagino que es porque hay menos hilos disponibles para realizar los cálculos de cada pixel, por lo que le toca a cada uno esperar a terminar con el suyo para continuar con el siguiente. En otras palabras, hay menos trabajadores en la cocina para sacar las órdenes.  

🌿
>

