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

🌱 **¿Qué ocurre si cambias el número de hilos a un número menor?**  
> Estaba usando 12. Lo cambié a 2. Mi guess es que se va a demorar más. Al ejecutarlo con los 12 hilos, se demoró `0.034 s`, mientras que con 2 se demoró `0.096 s`. La diferencia es imperceptible para mí, pero OBVIO se demoró mucho más en completar los cálculos. Me imagino que es porque hay menos hilos disponibles para realizar los cálculos de cada pixel, por lo que le toca a cada uno esperar a terminar con el suyo para continuar con el siguiente. En otras palabras, hay menos trabajadores en la cocina para sacar las órdenes.  
> Me das más experimentos? escríbelas como si fueras yo, con mi mismo lenguaje y redacción. Haz el predict, y explica (como principiante) por qué crees que sucede.  

🌿 **¿Qué ocurre si cambias el número de hilos a un número mayor?**  
> Tengo miedo porque no quiero que me crashee el PC D:. Mi guess es que... todo se va a poner lento y se va a demorar más, porque asumo que esos 12 eran lo más óptimo para el hardware de mi PC. Lo cambié a 20. Lo que pasó fue que se demoró `0.047 s`, más que con los 12 hilos. No me crasheó el PC ni tuvo un mega drop de fps. Mi guess es que sucede porque mi PC solamente puede alocar 12 núcleos, entonces igual también les toca esperar a cada uno para hacer el trabajo que están pidiendo de 20.  

🌼 **¿Qué pasa si aumento MUCHO las iteraciones?**  
> Voy a cambiar maxIterations de 100 a 500. Creo que va a tener más detallito y colorcitos. Para poder ver la diferencia, hice que el botón de n, en lugar de settearlo a 0, lo hiciera a 500. El resultado fue que, efectivamente, los colorcitos cambiaron y salieron algunos más vibrantes en los bordes y el rojo. No hay mucho más detalle, porque ya estaba muy detallado, pero sí se nota un cambio si los ejecuto con espacio y n así rápido para hacerle lado a lado.  

🌻 **¿Y si hago la ventana más grande?**  
> Voy a cambiar imgWidth y imgHeight al doble. Más píxeles = más trabajo para todos los hilos. Lo cambié a 1920 x 1080. Mi predict es que se demora más. Al ejecutarlo, efectivamente, pasó de los `0.034 s` a `0.103 s`... un cambio grandecito D:  

___

## 📝 Actividad 04

🌱 **¿Cuál es la estructura de datos principal que contiene la información de todos los boids y que es accedida por múltiples hilos (el hilo principal para dibujar, el hilo trabajador para actualizar)?**  
> La estructura principal es std::vector<Boid> boids dentro de la clase Flock, que tiene todos los boidcitos.  
  
🌿 **Observa la función Flock::threadedFunction() donde el hilo trabajador calcula el movimiento. ¿Qué operaciones realizan sobre el vector de boids compartido?**  
> como mencionaste en la explicación, cada boidcito tiene que leer los datos de los otros boids para poder calcular sus vectores y eso... pero sería peligroso si no tuviera ese lock, porque otros boidcitos podrían acceder y modificarlo al mismo tiempo, dañando esos cálculos de posición, dirección, cohesión y esas cositas.  

🌼 **Observa la función ofApp::draw(). ¿Qué operación realiza sobre el vector compartido?**  
> recorre ese vector para dibujar todos los boids.  

🌻 **Observa Flock::addBoid() y ofApp::mouseDragged(). ¿Qué operación realizan?**  
> `Flock::addBoid()` añade un nuevo boid al final del vector usando emplace_back()  
> `ofApp::mouseDragged()` llama a addBoid() cuando arrastramos el mouse  
  
🌱 **Describe un escenario específico y concreto donde la falta de sincronización podría causar un problema.**  
> 1. Hay un boidcito 1 leyendo el vector de boids para calcular su separación al boid pepito en la posición #3 del vector de boids.  
> 2. Yo hago drag y salen 2 boidcitos más.  
> 3. El vector de boidcitos se actualiza y tiene que cambiar sus cositas en la memoria (creo).  
> 4. La referencia que estaba usando boidcito 1 para calcular su separación de pepito explota y el programa tiene un error.
> Tener un lock/unlock en el add y el threadedfunction evita que ese tipo de cambios se realicen ANTES de que boidcito 1 termine de recalcular.  

🌼 **Localiza todas las llamadas a lock() y unlock() dentro de la clase Flock (o donde se acceda al vector compartido).**  
> En `threadedFunction():`  
```
lock();
for (Boid& b : boids) {
    b.run(boids);
}
unlock();
```
> En `addBoid():`
```
lock();
boids.emplace_back(x, y);
unlock();
```
> En `ofApp::draw()`
```
    flock.lock();
    for (Boid& b : flock.boids) {
        b.draw();
    }
    flock.unlock();
```

🌻 **Aunque los locks aseguran la correctitud, ¿Puedes intuir por qué tener muchos hilos esperando para adquirir un lock sobre el mismo vector (alta contención) podría limitar el beneficio de rendimiento del paralelismo en este caso? Justifica tu respuesta.**  
> Aunque tenga muchos trabajadores, a todos les tocaría hacer fila uno por uno para usar el horno del PC. Estoy perdiendo plata contratando más gente que no puede hacer nada porque tengo un solo horno. Lo mismo pasaría con los hilos, que están limitados por un solo lock a un solo vector.  

🌱 **¿Qué pasaría si tuviéramos varios hilos que calculan el movimiento de los boids? ¿Cómo podrías implementar esto? ¿Qué problemas crees que podrían surgir? ¿Cómo podrías solucionarlos?**  
> Podría dividir los boids en grupos y que cada hilo calcule solo su grupo. PERO el problema es que cada boid necesita información de TODOS los vecinos cercanos, no solo de su grupito... entonces flop. Podría también hacer que cada hilo calcule una de las cositas diferentes (un hilo para separación, otro para alineación, etc.) pero no sabría bien cómo sincronizarlo D:  
  
🌿 **Analiza el código del Flocking sin hilos y el Flocking con hilos. ¿Qué diferencias encuentras? ¿Por qué crees que es importante la sincronización en el segundo caso?**  
> Sin hilos, los FPS me dropearon a 20 con MUY poquitos boids. Con hilos, droppeó a 20 al llegar a los miles. Hay más responsividad!! es importante la sincronización para que los boids puedan actualizar sus datos correctamente, porque todo el concepto del programa depende de la exactitud a la hora de agruparse y hacer esas cositas chéveres de flock.  

🌼 **¿Por qué al añadir un nuevo boid la simulación se ralentiza? ¿Qué ocurre si añades muchos boids?**  
> Creo que es porque al añadir un nuevo boicito, todos los boids tienen que actualizar sus datos respecto a ese. Y si hay MUCHOS boids, hay +3 cálculos qué realizar por CADA uno de los boids instanciados, o sea que es súper exponencial.  

🌻 **Notaste que la versión con hilos tiene un sleep(5) en el hilo trabajador. ¿Por qué crees que se ha añadido? ¿Qué pasaría si lo eliminamos?**  
> Síii. Creo que es como algo parecido a lo del micro:bit, para no matar la CPU con trabajo constante. Es un intervalo súper chiquito de tiempo, pero igual eso le debe aliviar un poquito. Sin el sleep, creo que el hilo trabajador correría lo más rápido posible, consumiendo un núcleo completo al 100%.  
  
🌿 **Compara el rendimiento de ambos enfoques. ¿Cuál crees que es más eficiente? ¿Por qué?**  
> Eficiente, creería que el que no tiene hilos (si son poquitos boids), porque no genera cuellos de botellas... pero eficaz, diría que el de hilos, porque tiene mayor responsividad y soporta más boids sin empezar a droppear frames.  

🌼 **El uso de lock y unlock en la versión con hilos es crucial para evitar condiciones de carrera. ¿Qué pasaría si no se usaran? ¿Cómo afectaría esto al comportamiento del programa? (No olvides por favor que las condiciones de carrera son difíciles de reproducir, así que no te preocupes si no puedes verlas en acción).**  
> que pasen crasheos aleatorios, boids que se teletransportan o tienen como espasmos de dirección, comportamientos raritos en general como si los boids fueran esquizofrénicos D:  
  
___
