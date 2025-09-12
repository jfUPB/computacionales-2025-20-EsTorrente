# Bitácora de aprendizaje de la unidad 5

## 1.  **Diagnóstico inicial**
🌱 **¿Qué es el encapsulamiento para ti? Describe una situación en la que te haya sido útil o donde hayas visto su importancia.**  
> El encapsulamiento es una forma de proteger los datos y procesos de un programa. Permite restringir el acceso a ellos, controlando qué cambios pueden ser realizados.  
  
🌿 **¿Qué es la herencia? ¿Por qué un programador decidiría usarla? Da un ejemplo simple.**  
> Herencia se refiere a cuando tenemos una superclase con atributos y métodos preestablecidos, y definimos que una clase distinta (subclase) va a asumir esas mismas características y procesos, adaptándolos a su funcionamiento si es necesario. Una persona podría elegir utilizarla, por ejemplo, para crear un sistema de creación de enemigos. Todos los enemigos tienen un atributo de vida, ataque, defensa, y un método para atacar, morirse y huir. Teniendo una superclase de enemigo, podrías crear muchas variaciones de subclases (goblins, dragones, ladrones, etc...), cada uno compartiendo la misma estructura base. La superclase no se instancia, sólo está ahí como un blueprint para las subclases.  
  
🌼 **¿Qué es el polimorfismo? Describe con tus palabras qué significa que un código sea “polimórfico”**  
> Polimorfismo se refiere a la capacidad de distintos objetos de realizar el mismo método con procedimientos distintos, teniendo comportamientos únicos a los demás de su superclase. En el ejemplo anterior, todas las subclases de enemigos tienen los mismos atributos y métodos heredados, pero están realizando distintas acciones en atacar y huir. El método posee el mismo nombre y concepto, pero es realizado de manera diferente por cada clase que lo asume.  

### **Parte 2: Análisis del código**
🌱 **Señala una línea de código que sea un ejemplo claro de encapsulamiento y explica por qué lo es. ¿Por qué crees que el campo nombre es private pero la propiedad Nombre es public? ¿Qué problema se evita con esto?**  
```
private string nombre;

public string Nombre
    {
        get { return nombre; }
        protected set { nombre = value; }
    }
```
> Es un ejemplo claro de encapsulamiento porque toma una variable privada (que no se puede acceder por fuera del objeto), crea una variación de acceso público, y define una manera segura de ver el valor de la variable protegida y también modificarla. Evita alterar directamente la original, y permitiría confirmar que el valor que se quiere asignar sea válido antes de realizar el cambio.  
  
🌿 **¿Cómo se evidencia la herencia en la clase Circulo? Un objeto de tipo Circulo, además de Radio, ¿Qué otros datos almacena en su interior gracias a la herencia?**  
> Se está diciendo que Circulo es una subclase de Figura. Figura tiene simplemente un atributo para su nombre, y un método vacío de dibujar que DEBE ser reescrito por cualquiera de sus subclases para adaptarlo a sí mismo porque está definido como abstract. La clase Circulo agrega una variable propia (radio). Luego, en el constructor, toma el atributo heredado por la superclase (el nombre) y lo define junto al radio. Del mismo modo, hereda el método Dibujar y lo reescribe con "override", adaptándolo a su necesidad. Todo lo que contenía Figura, lo contiene Círculo también.  
  
🌼 **Observa el bucle foreach. La variable fig es de tipo Figura, pero a veces contiene un Circulo y otras un Rectangulo. Cuando se llama a fig.Dibujar(), el programa ejecuta la versión correcta. En tu opinión, ¿Cómo crees que funciona esto “por debajo”? No necesitas saber la respuesta correcta, solo quiero que intentes razonar cómo podría ser.**  
> En la lista se están agregando 3 figuras distintas, cada una con su método modificado de Dibujar. Los 3 métodos tienen el mismo nombre, pero procesos distintos por dentro. El foreach está recorriendo todos los elementos de la lista, y en cada uno se está ejecutando el método que encuentre con ese nombre. Como el método en todos se llama igual, y fig va cambiando dependiendo de el elemento de la lista que está recorriendo, entonces se llama ESPECÍFICAMENTE el método modificado de esa figura actual. Una vez llamado, el foreach continúa su recorrido por la lista y llama el mismo método personalizado de la siguiente figura en la lista. Si se agregaran más figuras, continuaría haciendo lo mismo para todas hasta terminar.

### **Parte 3: hipótesis sobre la implementación**
🌱 **Memoria y herencia: cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?**
> Me imagino que están almacenados en espacios consecutivos de la memoria... no creo que se ubiquen en posiciones muy distintas. Creería que primero pone el nomebre, porque es lo primero que se define en el constructor al ser heredado de la superclase, y luego pone los demás atributos en el mismo orden en el que se definen. Sin embargo, no estoy 100% segura.  
  
🌿 **El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.**
> Yo recuerdo de la clase de POO que podíamos ver la clase de un objeto con GetType(). Me imagino que eso es muestra de que el computador guarda los objetos como con un tipo de etiqueta que le dice la clase a la que pertenece, porque ya sé que con esa línea de código puedo buscarlo. Creería que al ejecutar el código, se está checkeando esa etiqueta de la figura actual.  
  
🌼 **La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?**
> Yo creo que se revisa mientras se está escribiendo el código y no te dejaría ejecutarlo si intentas acceder directamente a la bariable privada por fuera de la clase. Lo creo así principalmente porque mientras programábamos cositas en unity para el segundo semestre (y yo estaba apenas aprendiendo), constantemente se me olvidaba poner públicas las variables que iba a acceder desde otros scripts. El error saltaba de inmediato, me avisaba que no podía acceder a ella, y una vez modificaba y actualizaba el script con la variable, el error desaparecía completamente. Si no lo corregía, el programa directamente no se ejecutaba o crasheba cuando llegaba a la parte donde se usaba el script que intentaba acceder a la variable privada. No estoy segura de cómo el computador lo logra. Me imagino que, por ende, tiene que ser un check que hace el computador constantemente para revisar si tiene los permisos necesarios para obtener la info de esa otra clase.
    
___

## Actividad 02

> 🌱 El programa tiene una superclase de partícula, y unas subclases de partículas con distintos comportamientos. Tiene varios métodos de tipo virtual, lo que significa que cada subclase puede decidir si modificarlos o mantenerlos igual en su implementación individual.  

> 🌿 Para  RisingParticle (subclase de Particle), creo que está creando una partícula con un tiempo de vida definido que va subiendo en la pantalla de a poquito. El programa cuenta cuánto tiempo lleva después de haber spawneado. Si el tiempo de vida ya llegó al máximo, o alcanzó la altura definida como threshold, entonces la partícula explota.  

> 🌼 En ExplosionParticle (subclase de Particle), es casi el mismo concepto. Aquí se está tomando el tiempo que lleva la partícula de explosión viva. Si el tiempo supera la vida máxima, entonces se dice que la partícula muere. La transparencia de la partícula se va actualizando, utilizando ofMap() para definir que al inicio de la vida tendrá la saturación al full, y cuando alcance la vida máxima será 0.  

> 🌻 Para CircularExplosion (subclase de ExplosionParticle), se está definidiendo un patrón circular de la explosión usando senos y cosenos. Para RandomExplosion (subclase de ExplosionParticle), creo que simplemente se está definiendo una dirección random para estallar. Sin embargo, en el override de draw, veo que ya no se está dibujando la partícula con forma de círculo sino de rectángulo. En StarExplosion (subclase de ExplosionParticle), creo que se está dibujando la partícula con forma de estrella en la que el radio interno y externo aumentan con el tiempo.   

> 🌱 Luego, en ofApp.cpp, se están actualizando todas las partículas en cada frame. Usando el método definido en la clase Particle para ExplosionParticle y RisingParticle, si se cumple la condición de que deba estallar, escoge un patrón random de las 3 opciones. Le asigna un número random de partículas de la explosión, las instancia y las va borrando (tanto la original como las del efecto).  

> 🌿 Creo que las partículas rising se están instanciando al hacer clic o presionar espacio. Si se presiona la S, se guarda un screenshot del programa.

___

## Actividad 04

🌱 **Ejecuta este código. Luego, descomenta las líneas que están comentadas y vuelve a compilar. ¿Qué sucede? ¿Por qué sucede esto? ¿Qué puedes concluir?**  
> Al ejecutarlo por primera vez, no da ningún problema. El programa se ejecuta con normalidad porque solamente está intentando acceder a la variable pública de la clase AccessControl. Al descomentarlas, inmediatamente lanza un error que no permite completar la compilación (como lo había predecido en actividades anteriores). Sucede porque las variables de la clase AccessControl a la que está intentando acceder son:  
> 1. Protected: que significa que solamente sus subclases y ella misma van a poder verla y modificarla.  
> 2. Private: que dice que solamente su misma clase puede tocarla.
  
🌿 **Ahora quiero que notes algo. El encapsulamiento solo lo podemos garantizar en tiempo de compilación. Sin embargo, en tiempo de ejecución podemos acceder a los campos privados de un objeto. Analiza el siguiente programa. Compila el programa. ¿Qué pasa?**  
> Se está intentando hacer print de una variable privada. Lanza un error y no permite depurarlo. Si se comenta esa línea, el método público mostraría los valores sin problema.
  
🌼 **Ahora prueba con este programa. ¿Qué pasa?**  
> Se está utilizando un puntero para acceder directamente al valor almacenado en la variable original sin lanzar un error. Veo que hace un puntero para cada variable, y para los punteros del float y el char está sumándole +1 al valor del anterior... por lo que podría concluir que, como mencioné también en puntos anteriores, las variables se almacenan en posición consecutiva en la memoria.  
  
> Diría que el encapsulamiento es una manera de prevenir accidentes a la hora de acceder a valores en la memoria. Es una forma de proteger los datos, permitiendo un control riguroso de cada acción que se realiza sobre una variable. Es importante porque sabemos que los usuarios (y programadores) suelen realizar acciones impredecibles sin guiarse necesariamente por las indicaciones que damos, y esto permite restringir su capacidad de ingresar datos inválidos y dañarlo todo :(

___

## Actividad 05

🌱 ****  
> 
  
🌿 ****  
> 
  
🌼 ****  
> 

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
