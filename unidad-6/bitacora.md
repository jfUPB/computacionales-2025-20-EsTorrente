# Bitácora de aprendizaje de la unidad 6

### 📝 Actividad 1
🌱 **¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.**
<a name="Capturas"></a>
> `Tecla a`: atrae a las partículas hacia la posición del mouse. Como si fuera un campo gravitacional.
  
<img width="867" height="651" alt="image" src="https://github.com/user-attachments/assets/9328fca2-8563-4bb0-8f58-2db61eaf45aa" />  
  
> `Tecla r`: repele a las partículas, haciendo que "huyan" de la posición del mouse. Como si fuera un imán con otros del mismo polo, ejerciendo una fuerza en dirección opuesta.
  
<img width="1013" height="756" alt="image" src="https://github.com/user-attachments/assets/ba9f7562-cce2-4dac-bf95-3343101789af" />
  
> `Tecla s`: detiene a las partículas. Hace que se congelen en la posición actual y no reaccionen al mouse hasta actualizar de nuevo el efecto.
  
<img width="1014" height="757" alt="image" src="https://github.com/user-attachments/assets/10adc41a-350b-4c61-b62f-bc5a6d484e16" />
  
> `Tecla n`: el estado default. Las partículas flotan en direcciones random y con velocidades distintas. No tiene interacción con el mouse.
  
<img width="1012" height="760" alt="image" src="https://github.com/user-attachments/assets/15dbf74d-2e4f-4bef-81e9-2f4ed8e86664" />
  
🌿 **¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?**
> Como tal, la clase partícula no tiene subclases. Lo que hace que sean varios tipos es que en la creación de las partículas se le asignan distintos atributos. En el OffApp.cpp sí se inician las partículas como conjunto con unos atributos base, pero luego, desde el setup, se le está diciendo al programa que cree 100 partículas star, 5 shooting stars, 10 planets con el método `createParticle`. En ese método se modifican los atributos default de acuerdo al string con el que se envió la partícula al método. Para star, solamente cambian su tamaño y su color. Para shooting star, cambian su tamaño, su color y se le asigna una mayor velocidad (se multiplica la default x 3). Para planets, sólo se modifica su color y su tamaño. En ese sentido, sí podría decirse que la clase Particle se inicia con el mismo comportamiento, pero es inmediátamente modificado en setup.  

🌼 **Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.**  
> Puse las capturas [aquí, en la primera pregunta](#Capturas). 

🌻 **¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.**
> En el estado de stop, la velocidad es 0 (no hay movimiento). En el estado normal, se le asigna una velocidad random que se le suma a su posición. Para repelerla y atraerla, me imagino que la posición de la partícula está siendo sumada o restada por la posición del mouse... al mismo tiempo, creo que la velocidad se estaría multiplicando por el valor de una fuerza que actúa sobre ella.

___

### 📝 Actividad 2
🌱 **Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?**
> El patrón Observer provoca que las clases dependan menos entre ellas, lo que es bueno porque significa menor acoplamiento. Además, como mencionaste en la clase, permite que muchas personas trabajen en sus clases separadas sin tener que esperar a recibir los avances de los demás, sino que todo puede adelantarse y simplemente ponerse de acuerdo en la interfaz del Observer.  
  
🌿 **Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.**
<img width="1162" height="660" alt="image" src="https://github.com/user-attachments/assets/fa257073-6a83-4767-bed7-31e3b4523cb6" />  
   
🌼 **Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.**  
<img width="978" height="829" alt="image" src="https://github.com/user-attachments/assets/c1596543-3fff-4834-8b7e-6293fbd939dd" />  

🌻 **¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.**
> ofApp tendría que tener acceso a las variables internas de cada particle, estaría haciendo demasiadas tareas solita y se enreda si se quieren agregar comportamientos diferentes. Con el observer, el ofApp nada más manda notificación y las partículas ven cómo reaccionan por su cuenta. Cada clase queda con poquitas responsabilidades, y además, el sistema de notificaciones es útil para otras funciones si se quieren implementar en el futuro.

___

### 📝 Actividad 3
🌱 **Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?**
> Simplifica mucho el proceso de creación de objetos. No deja códigos new en todas partes, sino que encapsula todo en un método que se encargue de separar las distintas variaciones posibles y cómo instanciarlas. El problema principal que soluciona es que si hay que hacer modificaciones, arreglar código, hacer debug o agregar un tipo nuevo de partícula, es MUCHÍSIMO más fácil sólo revisar un método en una clase, que irse a buscar un montón de métodos chiquitos súper parecidos en miles de clases.  
  
🌿 **¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.**
> Le permite al ofApp seguirse concentrando en una sola función: recibir inputs y mandar notificaciones, fin. Es bueno que en un código, cada método y cada clase tenga funciones muy específicas. ParticleFactory tiene solo una función: instanciar los distintos tipos de partículas, fin. Gracias a eso, como mencioné antes, es muchísimo más fácil realizar modificaciones y adiciones al código.  
   
🌼 **Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?**  
> Síp! para que en el setup le diga cuántas de esas partículas crear en el ParticleFactory. Es solamente agregar otro for donde se le indique la cantidad... pero lo de cambiar los atributos del tamaño, color y velocidad sería TODO en el ParticleFactory, ahí no se tiene que tocar el setup en absoluto. O sea, no tengo que cambiar nada de la lógica... solamente copi pastear y cambiar el nombre de la partícula.  

🌻 **El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.**
> Lo bueno es que no toca instanciar para nada un ParticleFactory, sino que se puede llamar de una al método. Lo malo es que no se le puede hacer override, lo que significa que no se puede meter polimorfismo, porque ese método lo comparte toda la clase... no cada instancia.

___

### 📝 Actividad 4
🌱 **Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?**
> En vez de tener un montón de ifs o switchs que checkeen un montón de estados posibles, permite encapsularlos todos. Se implementan cuando un objeto tiene que hacer cambios internos tan drásticos que hasta parecen una clase diferente. También te da la capacidad de definir transiciones entre los estados (al entrar y salir de ellos).   
  
🌿 **Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).**  
<img width="1086" height="450" alt="image" src="https://github.com/user-attachments/assets/24dec6db-17e9-482f-9af1-028e105f50e3" />  
  
🌼 **Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).**  
> Otra vez volvemos a que cada clase debe tener funciones muy específicas, todo debe tener el menor grado de acoplamiento posible, no deben depender unas de otras, y NO SE DEBE TENER QUE ABRIR EL PARTICLE PARA MODIFICARLO!! entonces, tener un montón de switch o ifs dentro de esa clase probocaría que:  
> 1. Tocara abrirla para quitar/agregar estados, lo cuál va en contra del principio.  
> 2. Particle tenga muchísimas tareas y checks y cosas por estar revisando.  
> 3. el código sea maluco de leer.  
> Usar el patrón state hace que todo sea más bonito, modular, fácil de modificar y siga los principios de POO.  

🌻 **¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?**
> Tienen la responsabilidad de preparar las partículas para los cambios entre estados. Si no se resetean o actualizan datos al entrar y salir de algunos estados, puede dañar el funcionamiento de los demás. También puede servir simplemente por estética, para agregar algún comportamiento que indique o suavice la transición. Por ejemplo, en el onEnter de AttractState, podría hacer que todas las bolitas cambien de color a uno mismo para simbolizar que son como una mente colmena... y para el onExit del stopState, podría hacer una animación chiquita donde cada partícula se hace un poquito más grande y después regresa a su tamaño original antes de retomar su movimiento, para que no se vea tan drástico el cambio de estar congelado a moverse. También podría servir para poner logs que permitan revisar esos cambios.  

