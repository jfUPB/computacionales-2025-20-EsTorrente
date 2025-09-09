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
>
  
🌿 **El mecanismo del polimorfismo: pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.**
>
  
🌼 **La barrera del encapsulamiento: ¿Cómo crees que el compilador logra que no puedas acceder a un miembro private desde fuera de la clase? ¿Es algo que se revisa cuando escribes el código, o es una protección que existe mientras el programa se ejecuta? ¿Por qué piensas eso?**
>
  
___

## 2.  **La pregunta inicial**

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
> [!CAUTION]
> Esta sección es OBLIGATORIA y central para tu evaluación
