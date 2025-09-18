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
```program.cpp
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

⭐ **MI CONCLUSIÓN:** ⭐
> Creo que estoy bien de conceptos previos. Sí me quedo con la duda sobre cómo es exactamente que se sabe cómo llamar a cada método en el polimorfismo, pero creo que en definiciones e ideas bases tengo lo suficiente como para realizar la unidad sin problemas.  
    
___

Estoy tomando la ruta guiada, por lo que mis preguntas son las que tú planteas + cualquier otra que me vaya surgiendo...  

## Actividad 02

> 🌱 El programa tiene una superclase de partícula, y unas subclases de partículas con distintos comportamientos. Tiene varios métodos de tipo virtual, lo que significa que cada subclase puede decidir si modificarlos o mantenerlos igual en su implementación individual.  

> 🌿 Para  RisingParticle (subclase de Particle), creo que está creando una partícula con un tiempo de vida definido que va subiendo en la pantalla de a poquito. El programa cuenta cuánto tiempo lleva después de haber spawneado. Si el tiempo de vida ya llegó al máximo, o alcanzó la altura definida como threshold, entonces la partícula explota.  

> 🌼 En ExplosionParticle (subclase de Particle), es casi el mismo concepto. Aquí se está tomando el tiempo que lleva la partícula de explosión viva. Si el tiempo supera la vida máxima, entonces se dice que la partícula muere. La transparencia de la partícula se va actualizando, utilizando ofMap() para definir que al inicio de la vida tendrá la saturación al full, y cuando alcance la vida máxima será 0.  

> 🌻 Para CircularExplosion (subclase de ExplosionParticle), se está definidiendo un patrón circular de la explosión usando senos y cosenos. Para RandomExplosion (subclase de ExplosionParticle), creo que simplemente se está definiendo una dirección random para estallar. Sin embargo, en el override de draw, veo que ya no se está dibujando la partícula con forma de círculo sino de rectángulo. En StarExplosion (subclase de ExplosionParticle), creo que se está dibujando la partícula con forma de estrella en la que el radio interno y externo aumentan con el tiempo.   

> 🌱 Luego, en ofApp.cpp, se están actualizando todas las partículas en cada frame. Usando el método definido en la clase Particle para ExplosionParticle y RisingParticle, si se cumple la condición de que deba estallar, escoge un patrón random de las 3 opciones. Le asigna un número random de partículas de la explosión, las instancia y las va borrando (tanto la original como las del efecto).  

> 🌿 Creo que las partículas rising se están instanciando al hacer clic o presionar espacio. Si se presiona la S, se guarda un screenshot del programa.


<a name="captura1"></a>
<img width="1011" height="751" alt="image" src="https://github.com/user-attachments/assets/12ab0833-1a90-4902-85c8-b0900aabe676" />

<img width="956" height="741" alt="image" src="https://github.com/user-attachments/assets/80cb1ff4-0df6-4cdd-a44f-52cdf5cf7179" />

<img width="1008" height="748" alt="image" src="https://github.com/user-attachments/assets/c035df3f-005f-4630-9f8b-5edd03fd39e7" />


___

## Actividad 03

🌱 **Antes de ejecutar el experimento, ¿Qué esperas ver en memoria (hipótesis)? Ejecuta el código y muestra una captura de pantalla del objeto en la memoria. ¿Qué puedes observar? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir?**  
> En el código veo `std::vector<Particle*> particles;`. El * me hace creer que voy a ver un puntero de algún tipo que apunte a los atributos (creo?) de la clase instanciada. También me imagino que la jerarquía en la que va a aparecer es: primero los datos de la superclase, después los datos de la subclase. Y si explota, entonces supongo que mirando el risingParticle, sería algo así:
> - RisingParticles  
>   - Particles  
>     - Atributos de clase Particles  
>   - atributos de clase RisingParticles
  
Lo que vi en el depurador fue esto:
<img width="917" height="399" alt="image" src="https://github.com/user-attachments/assets/b681c0d2-983b-4f73-879d-7274e1fd9bbf" />
  
> Efectivamente, va primero RisingParticles, después Particles, un puntero, y luego los atributos de RisingParticles. El depurador me deja ver todos los valores con los que fue instanciada la partícula. Además, el hecho de que la jerarquía sea [0] -> [RisingParticles] me está indicando que esa sola partícula es el primero y único objeto instanciado por ahora en el vector. El programa llegó al breakpoint en el momento en el que la partícula fue creada, por lo que su vida es 0 y no ha explotado aún. Si se hubiera capturado cuando exploded = true, me imagino que en la jerarquía habría también unas partículas de explosión junto a la de rising. Para confirmarlo, modifiqué el bool de `RisingParticle -> exploded para ser seteado en true.` El resultado fue este:  
<img width="914" height="309" alt="image" src="https://github.com/user-attachments/assets/fb155251-431f-4d0c-8c3b-fa2500527e7f" />
  
> Estuve casi en lo correcto. Sí se crearon todas las partículas de la explosión dentro del vector, pero no caí en cuenta de que la partícula rising inicial se habría destruido. Además, noto que todos los CircularExplosion creados en el vector tienen una dirección similar de memoria (igual hasta `0x00...36c3`), pero los __vfptr para TODAS las partículas de explosión fue siempre `0x00...14056bb30`.
   
🌿 **Usa de nuevo el depurador para capturar un objeto de tipo CircularExplosion. Es posible que tengas que hacer modificaciones mínimas en el código para que puedas capturar este objeto más fácilmente. Observa con el depurador la ventana de Auto o Locals y la ventana de Memory 1. Trata de buscar en memoria todas las partes que componen al objeto tipo CircularExplosion ¿Qué puedes observar en la memoria? ¿Qué información te proporciona el depurador? ¿Qué puedes concluir? NO OLVIDES tener a la mano todas la jerarquía de clases que componen a CircularExplosion. De esta manera podrás identificar cada parte del objeto en memoria.**  
> La modificación que hice para poder lanzarlo fue llamar `createRisingParticle()` (al que le cambié el nombre para `createCircularExplosion()` porque tú nos regañaste por no hacer eso en la actividad del micro:bit) desde el Setup() para asegurarme de que saliera una sola partícula, e intercambiar el particles.push_back que instanciaba el risingParticle por `particles.push_back(new CircularExplosion(pos, col))`. Puse un breakpoint después del draw(). La consola me quedó así:
  
<img width="935" height="374" alt="image" src="https://github.com/user-attachments/assets/2c20e2c0-037f-4683-9566-d9ba9cf4f317" />  
  
> La jerarquía es CircularExplosion -es una-> ExplosionParticle -es una-> Particles. Aunque en el depurador puede parecer que va al revés por el orden en el que sale y que las superclases están como "contenidas" dentro de CircularExplosion, tiene sentido que se pongan los datos de esa manera. Igualmente, los datos heredados de la mayor superclase siempre está saliendo de primera, lo cuál yo asumo que es porque son los primeros datos que se guardan en la memoria al llamar al constructor. El value que sale al lado del [0] sería, si no estoy mal, la posición de la memoria donde se está instanciando el objeto. Otra cosa que estoy notando es que ese [0] es de tipo `Particle* {circularExplosion}`, lo cuál asumo que es una forma de decir que aunque el puntero apunta a una partícula, esa partícula es de subclase circularExplosion.    

🌼 **Captura la _vtable de un objeto CircularExplosion, pega la imagen en tu bitácora, pero observa detenidamente la tabla de funciones. ¿Qué puedes observar?**  
<img width="889" height="132" alt="image" src="https://github.com/user-attachments/assets/84340852-6794-41fa-b9a9-80bb343406a3" />  

> Puedo observar que la tabla parece ser como un tipo de vector con todos los métodos que ejecuta la partícula, y que su tipo es un puntero Void.  
  
🌻 **Ahora, captura en memoria la _vtable de un objeto StarExplosion, pega la imagen en tu bitácora y observa detenidamente la tabla de funciones.**  
<img width="889" height="167" alt="image" src="https://github.com/user-attachments/assets/e71d517e-be52-446d-a122-86cf8d9b2b62" />  

> Son los mismos métodos (porque esos los hereda de la superclase de Particles y no agrega ninguna nueva), pero se ve claramente que el draw que está llamando es ESPECÍFICAMENTE la versión que modificó la clase de starExplosion.  

🌱 **Observa de nuevo ambas tablas y compara. ¿Qué puedes ver? ¿Qué puedes concluir? ¿Qué relación existe entre la tabla de funciones y los métodos virtuales? Esta pregunta que te voy a hacer no es fácil y la idea de hacerla es prepararte mentalmente para lo viene ¿Para qué crees que pueda servir una tabla de funciones virtuales? Para responder esta pregunta trata de pensar en el polimorfismo con interfaces y clases abstractas que viste al estudiar C#**  
> Yo sé que cuando una superclase tiene un método definido, sus subclases deben heredarlas siempre, fijo. También sé que un método virtual le da la opción a cada clase individualmente de decidir si la van a modificar o mantener tal como la recibieron, sin obligarlos como lo haría un método static. Tanto el circularExplosion como el starExplosion tenían los mismos métodos en su tabla (porque los heredaron), pero veo que se está especificando directamente a CUÁL clase es a la que el puntero busca para ejecutar la versión correspondiente. Quería comparar las direcciones de memoria para ambas, entonces instancié las dos al mismo tiempo. Esto es lo que vi:  
<img width="909" height="322" alt="image" src="https://github.com/user-attachments/assets/120df057-e340-4c06-b068-a9b8e4f39c45" />
  
> Lo que descubrí es que la dirección de memoria para los métodos heredados no modificados ES LA MISMA PARA AMBOS!! pero para el método de draw(), que SÍ fue cambiado por cada clase, la dirección de memoria SÍ ES DIFERENTE!! por ende, asumiré que la tabla de direcciones es lo que permite identificar y ejecutar cuál es el método que se está llamando en la memoria, incluso si todas las subclases los comparten y simplemente modifican.
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

🌻 **En tus palabras, ¿Qué es el encapsulamiento? ¿Por qué es importante?**
> Diría que el encapsulamiento es una manera de prevenir accidentes a la hora de acceder a valores en la memoria. Es una forma de proteger los datos, permitiendo un control riguroso de cada acción que se realiza sobre una variable. Es importante porque sabemos que los usuarios (y programadores) suelen realizar acciones impredecibles sin guiarse necesariamente por las indicaciones que damos, y esto permite restringir su capacidad de ingresar datos inválidos y dañarlo todo :(

___

## Actividad 05

🌱 **¿Cómo se implementa la herencia en C++?**  
> Por lo que estoy viendo, es similar al C#. Los atributos heredados en el constructor se declaran de la misma manera, pero al usar los : después del nombre de la clase, hay que agregarle el public. Si no se agregan todos los métodos y atributos heredados, te tira error.    
> Por ende, queda así:
```program.cpp
class NombreSubClase : public NombreSuperClase {
public:
    NombreSubClase(atributos subclase)
        : NombreSuperClase(atributos heredados) {
        aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa;
    }

    void MétodoHeredado() override {
        AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA;
    }
};
```
> Aquí lo que aprendí cuando estaba buscando es que al parecer los métodos abstract NO existen en C++!! los reemplaza siempre un virtual!! la manera de hacerlo obligatorio es igualando la función a 0.
  
🌿 **C++ permite hacer algo que C# no: herencia múltiple. Realiza un experimento que te permita ver cómo se objeto en memoria cuya clase base tiene herencia múltiple.**  
Mi experimento:
```program.cpp
#include <iostream>

using namespace std;

// superclase 1
class Heroe {
public:
    int ataque;
    int defensa;

    Heroe(int ataque, int defensa) : ataque(ataque), defensa(defensa) {}

    virtual void pelear() = 0;

    virtual ~Heroe() {}
};

// superclase 2
class Enano {
public:
    string arma;

    Enano(string arma) : arma(arma) {}

    virtual void insultarElfo() {
        cout << endl << "And you know what this Dwarf says to that? Ishkhaqwi ai durugnul!" << endl;
        cout << endl << "El enano le apunta al elfo con su " << arma << endl;
    }

    virtual ~Enano() {}
};

// clase con la herencia de ambos
class Personaje : public Heroe, public Enano {
public:
    string nombre;

    Personaje(string nombre, int ataque, int defensa, string arma) : 
        Heroe(ataque, defensa), 
        Enano(arma),
        nombre(nombre)
    {}

    void pelear() override {
        cout << nombre << " pelea con un ataque de " << ataque << " y una defensa de " << defensa << "!" << endl;
    }

    ~Personaje() {}
};

int main() {
    cout << "=== EXPERIMENTO :D ===" << endl;

    Personaje gimli("Gimli", 85, 70, "hacha de batalla");

    gimli.pelear();
    gimli.insultarElfo();

    cout << endl << "=== FIN :D ===" << endl;

    return 0;
}
```
Al ejecutarlo:  
<img width="670" height="195" alt="image" src="https://github.com/user-attachments/assets/8056310d-c071-4a1e-93b2-3e4f6243bcbc" />  

Así se veía la consola:  
<img width="923" height="174" alt="image" src="https://github.com/user-attachments/assets/681d9ae2-cfe2-45e6-a64a-b3d0cdcc726c" />

> Tiene a Héroe y Enano en el mismo nivel de su jerarquía.  

Apliqué lo que descubrí en el punto anterior, e hice que el método de Héroe fuera obligatorio modificarlo. Si lo intento borrar, me tira este error:  
<img width="538" height="522" alt="image" src="https://github.com/user-attachments/assets/d0158da5-b691-44e6-b775-821ec2a55633" />  

Que me está diciendo que el método pelear de la clase héroe no tiene un override, y eso no es permitido porque lo igualé a 0.  
Me puse a buscar también que era lo que significaban los `::` porque los vi mucho en lo de openframeworks... y decía básicamente esto:   
> Se llama calificación de ámbito (o "scope resolution"). Es una forma de ser específico sobre exactamente qué versión de la función insultarElfo() quiero llamar. Le estoy diciendo al compilador que no quiero la versión de insultarElfo() que podría estar en esta clase o en cualquier otra. Quiero específicamente la versión que está definida en la clase Enano.
  
Después, quería revisar lo de las tablas. Creé otra clase Elfo, y otra clase Personaje2 que compartiera con héroe. Quedó así:
```program.cpp
#include <iostream>

using namespace std;

// superclase 1
class Heroe {
public:
    int ataque;
    int defensa;

    Heroe(int ataque, int defensa) : ataque(ataque), defensa(defensa) {}

    virtual void pelear() = 0;

    virtual ~Heroe() {}
};

// superclase 2
class Enano {
public:
    string arma;

    Enano(string arma) : arma(arma) {}

    virtual void insultarElfo() {
        cout << endl << "And you know what this Dwarf says to that? Ishkhaqwi ai durugnul!" << endl;
        cout << endl << "El enano le apunta al elfo con su " << arma << endl;
    }

    virtual ~Enano() {}
};

class Elfo {
public:
    string arma;

    Elfo(string arma) : arma(arma) {}

    virtual void insultarEnano() {
        cout << endl << "The Dwarf breathes so loud, we could have shot him in the dark." << endl;
        cout << endl << "El elfo le apunta al enano con su " << arma << endl;
    }

    virtual ~Elfo() {}
};

// clase con la herencia de ambos
class Personaje : public Heroe, public Enano {
public:
    string nombre;

    Personaje(string nombre, int ataque, int defensa, string arma) : 
        Heroe(ataque, defensa), 
        Enano(arma),
        nombre(nombre)
    {}

    void pelear() override {
        cout << nombre << " pelea con un ataque de " << ataque << " y una defensa de " << defensa << "!" << endl;
    }

    ~Personaje() {}
};

class Personaje2 : public Heroe, public Elfo {
public:
    string nombre;

    Personaje2(string nombre, int ataque, int defensa, string arma) :
        Heroe(ataque, defensa),
        Elfo(arma),
        nombre(nombre)
    {}

    void pelear() override {
        cout << nombre << " pelea con un ataque de " << ataque << " y una defensa de " << defensa << "!" << endl;
    }

    ~Personaje2() {}
};

int main() {
    cout << "=== EXPERIMENTO :D ===" << endl;

    Personaje2 haldir("Haldir", 100, 40, "arco");
    Personaje gimli("Gimli", 85, 70, "hacha de batalla");

    haldir.insultarEnano();
    gimli.insultarElfo();
    gimli.pelear();
    haldir.pelear();

    cout << endl << "=== FIN :D ===" << endl;

    return 0;
}
```
<img width="925" height="284" alt="image" src="https://github.com/user-attachments/assets/866cd0f7-1ce9-42aa-bd9b-1572e77f7608" />

> En la memoria, pelear es distinto para ambos... porque le estoy haciendo override! Y veo súper claro que se usa el scope resolution AL LADO DE LA DIRECCIÓN DE MEMORIA para decir cuál es el método que se llama!! :0 (`Personaje2::pelear(void)` y `Personaje::pelear(void)`)  
> pero si le quito el override y dejo el método como un virtual normalito, la memoria se ve así:
<img width="911" height="266" alt="image" src="https://github.com/user-attachments/assets/5c6e9012-064e-4d23-a598-072d25bf2473" />

> Ahora en ambos ya no se está usando el scope resolution de su subclase, sino el de la superclase Heroe!! (`Heroe::pelear(void)`)  
___ 

## Actividad 06
🌿 **¿Qué relación existe entre los métodos virtuales y el polimorfismo?**  
> Los métodos virtuales son lo que permite a las subclases heredar métodos y adaptarlos a sus necesidades individuales. Se junta con el cosito de los :: (ya se me olvidó el nombre D:) para definir cuál es el método específico que se debe llamar en cada clase.  
___ 

## Actividad 07
  
**Las adiciones que hice fueron:**  
1. Una partícula que spawnea con arrastrar mouse + su posición (no usé el concepto de la unidad pasada porque se explotan manualmente y no necesitaba cambiar el tamaño dependiendo del array, el efecto que quería era distinto).  
2. Una partícula de un cubito 3D que no se mueve, pero sí rota en su propio eje y palpita hasta que explota.  
3. No entendí si lo de "modo de explosión" era partícula o la condición que lo estalla, entonces hice las dos. Una partícula de explosión en forma de triángulo, e hice que todas las partículas de cubo explotaran el mismo tiempo al presionar b :D  
4. Puse que la partícula de cubito spawneara con la tecla "a", cambié el número de partículas de explosión a 1 para sólamente ver una en la consola y poderla analizar, y cambié el explosionType a 3 fijo (triangulito) para poder ver mi adición en específico. También tuve que agregarle a la clase ofApp el método público de `mouseDragged(int x, int y, int button)`, `createPulsingCubeParticle()` y `createMouseParticle(int x, int y)`. Cambié el código para que la risingParticle spawneara ya explotada, entonces en la consola no me sale la partícula rising spawneada sino directamente la de explosión. Por último, puse que spawneara fijo una partícula de cada uno de los tipos que agregue para poder poner un break después del primer draw y verlas igual :>    

Usé una partícula en 3D porque quería ver si había diferencias con todo lo 2D que hemos hecho. Una cosa que descubrí es que esas figuras tridimensionales no se dibujan como las 2D...  
Para la posición, se utiliza `ofTranslate(position)`. El problema es que eso me mueve el centro de TOOODAS las figuritas dibujadas, por lo que el draw en cada frame se descuadra horrible y daña todo. Entonces, para corregirlo, debo usar primero `ofPushMatrix()` que guarda las configuraciones anteriores de posición y rotación del centro general de todo, y ya después de haber dibujado el cubo, `ofPopMatrix()` que regresa a la confi normal. Vi que esto también lo usaste para la explosión de estrellita.  
  
🌼 **ofApp.h**
```
#pragma once
#include "ofMain.h"
#include <vector>

// -------------------------------------------------
// Clase base abstracta: Particle
// -------------------------------------------------
class Particle {
public:
    virtual ~Particle() {}
    virtual void update(float dt) = 0;
    virtual void draw() = 0;
    virtual bool isDead() const = 0;
    // Nuevo método para saber si la partícula (tipo RisingParticle) debe explotar
    virtual bool shouldExplode() const { return false; }
    // Métodos para obtener posición y color, para usarlos en explosiones
    virtual glm::vec2 getPosition() const { return glm::vec2(0, 0); }
    virtual ofColor getColor() const { return ofColor(255); }

    virtual void forceExplode() {} //le agrego esto para la otra forma de explotar que pides, pero solamente la del cubo la usa :P
    // como no lo igualo a 1 entonces no es obligación modificarlo
};

// -------------------------------------------------
// RisingParticle: Partícula que nace en la parte inferior central y sube
// -------------------------------------------------
class RisingParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float lifetime; // Tiempo máximo antes de explotar
    float age;
    bool exploded;
public:
    RisingParticle(const glm::vec2& pos, const glm::vec2& vel, const ofColor& col, float life)
        : position(pos), velocity(vel), color(col), lifetime(life), age(0), exploded(true) {
    }

    void update(float dt) override {
        position += velocity * dt;
        age += dt;
        // Aumenta la desaceleración para dar sensación de recorrido largo
        velocity.y += 9.8f * dt * 8;
        // Condición de explosión: cuando la partícula alcanza aproximadamente el 15% de la altura
        float explosionThreshold = ofGetHeight() * 0.15 + ofRandom(-30, 30);
        if (position.y <= explosionThreshold || age >= lifetime) {
            exploded = true;
        }
    }

    void draw() override {
        ofSetColor(color);
        // Partícula más grande
        ofDrawCircle(position, 10);
    }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return position; }
    ofColor getColor() const override { return color; }
};

// mis variaciones ================================================
class PulsingCubeParticle : public Particle {
protected:
    glm::vec3 position;
    ofColor color;
    float age;
    float baseSize;
    float pulseTimer;
    bool isPulsing;
    bool exploded;
    //no necesito lifetime

public:
    PulsingCubeParticle(const glm::vec3& pos, const ofColor& col)
        : position(pos), color(col), age(0), exploded(false), baseSize(15.0f), pulseTimer(0), isPulsing(false) {
    }

    void update(float dt) override {
        age += dt;

        pulseTimer += dt;
        if (pulseTimer > 0.7f) { //palpita cada 0.7 segundos
            pulseTimer = 0;
            isPulsing = true;
        }

        if (isPulsing && pulseTimer > 0.3f) { //palpita por 0.3 segundos
            isPulsing = false;
        }
    }

    void draw() override {
        ofSetColor(color);

        ofPushMatrix();

        ofTranslate(position);

        ofRotateYDeg(age * 60);
        ofRotateXDeg(45); 

        float currentSize = baseSize;
        if (isPulsing) {
            float pulseProgress = pulseTimer / 0.3f;
            float pulseSize = sin(pulseProgress * PI) * 10.0f; //para que loopee, porque sen(0) = 0, sen(pi/2) = 1, sen(pi) = 0
            currentSize += pulseSize;
        }

        ofDrawBox(0, 0, 0, currentSize);

        ofPopMatrix();
    }

    void forceExplode() override {
        exploded = true; //obliga a que estalle, no lo hace con el tiempo >:D
    }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return glm::vec2(position.x, position.y); }
    ofColor getColor() const override { return color; }
};

class MouseParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float lifetime;
    float age;
    bool exploded;

public:
    MouseParticle(const glm::vec2& pos, const ofColor& col, float life)
        : position(pos), color(col), lifetime(life), age(0), exploded(false) {
        velocity = glm::vec2(ofRandom(-50, 50), ofRandom(-50, 50));
    }

    void update(float dt) override {
        position += velocity * dt;
        age += dt;

        velocity *= 0.95f; //se vuelve lentica y queda quieta

        if (age >= lifetime) {
            exploded = true;
        }
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, 20);
    }

    bool isDead() const override { return exploded; }
    bool shouldExplode() const override { return exploded; }
    glm::vec2 getPosition() const override { return position; }
    ofColor getColor() const override { return color; }
};

// -------------------------------------------------
// Clase base para explosiones: ExplosionParticle
// -------------------------------------------------
class ExplosionParticle : public Particle {
protected:
    glm::vec2 position;
    glm::vec2 velocity;
    ofColor color;
    float age;
    float lifetime;
    float size;  // tamaño de la partícula de explosión
public:
    ExplosionParticle(const glm::vec2& pos, const glm::vec2& vel, const ofColor& col, float life, float sz)
        : position(pos), velocity(vel), color(col), age(0), lifetime(life), size(sz) {
    }

    void update(float dt) override {
        position += velocity * dt;
        age += dt;
        float alpha = ofMap(age, 0, lifetime, 255, 0, true);
        color.a = alpha;
    }

    bool isDead() const override { return age >= lifetime; }
};

// -------------------------------------------------
// CircularExplosion: Explosión en patrón circular
// -------------------------------------------------
class CircularExplosion : public ExplosionParticle {
public:
    CircularExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.2f, ofRandom(16, 32)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(80, 200);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }

    void draw() override {
        ofSetColor(color);
        ofDrawCircle(position, size);
    }
};

// -------------------------------------------------
// RandomExplosion: Explosión con direcciones aleatorias
// -------------------------------------------------
class RandomExplosion : public ExplosionParticle {
public:
    RandomExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.5f, ofRandom(16, 32)) {
        velocity = glm::vec2(ofRandom(-200, 200), ofRandom(-200, 200));
    }

    void draw() override {
        ofSetColor(color);
        ofDrawRectangle(position.x, position.y, size, size);
    }
};

// -------------------------------------------------
// StarExplosion: Explosión en forma de estrella
// -------------------------------------------------
class StarExplosion : public ExplosionParticle {
public:
    StarExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.3f, ofRandom(20, 40)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(90, 180);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }

    void draw() override {
        ofSetColor(color);
        int rays = 5;
        float outerRadius = size;
        float innerRadius = size * 0.5;
        ofPushMatrix();
        ofTranslate(position);
        for (int i = 0; i < rays; i++) {
            float theta = ofMap(i, 0, rays, 0, TWO_PI);
            float xOuter = cos(theta) * outerRadius;
            float yOuter = sin(theta) * outerRadius;
            float xInner = cos(theta + PI / rays) * innerRadius;
            float yInner = sin(theta + PI / rays) * innerRadius;
            ofDrawLine(0, 0, xOuter, yOuter);
            ofDrawLine(xOuter, yOuter, xInner, yInner);
        }
        ofPopMatrix();
    }
};

// mi variación =========================================================================
class TriangleExplosion : public ExplosionParticle {
public:
    TriangleExplosion(const glm::vec2& pos, const ofColor& col)
        : ExplosionParticle(pos, glm::vec2(0, 0), col, 1.0f, ofRandom(10, 20)) {
        float angle = ofRandom(0, TWO_PI);
        float speed = ofRandom(50, 150);
        velocity = glm::vec2(cos(angle), sin(angle)) * speed;
    }

    void draw() override {
        ofSetColor(color);
        float height = size * 1.732/2; //es la razón de un triángulo equilátero :P (lado * raíz de 3/2)
        ofDrawTriangle(
            position.x, position.y - height / 2, //vértice de arriba
            position.x - size / 2, position.y + height / 2, //vértice izquierdo abajito
            position.x + size / 2, position.y + height / 2 //vértice derecho abajito
        );
    }
};

// -------------------------------------------------
// ofApp: Manejo de la escena y eventos
// -------------------------------------------------
class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();
    void mousePressed(int x, int y, int button);
    void mouseDragged(int x, int y, int button); //añadido para que funcione la otra partícula :>
    void keyPressed(int key);

    std::vector<Particle*> particles;
    ~ofApp();

private:
    void createRisingParticle();
    void createPulsingCubeParticle();
    void createMouseParticle(int x, int y);

};
```

🌻 **ofApp.cpp**  
```aaaaaa.cpp
#include "ofApp.h"

// --------------------------------------------------------------
void ofApp::setup() {
    ofSetFrameRate(60);
    ofBackground(0);
    createPulsingCubeParticle();
    createMouseParticle(20,20);
    createRisingParticle();

}

// --------------------------------------------------------------
void ofApp::update() {
    float dt = ofGetLastFrameTime();

    // Actualiza todas las partículas
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->update(dt);
    }

    // Procesa las partículas (iteración en reversa para facilitar eliminación)
    for (int i = particles.size() - 1; i >= 0; i--) {
        // Si la partícula debe explotar, generamos nuevas explosiones
        if (particles[i]->shouldExplode()) {
            int explosionType = (3); // lo cambio para testear fijo el triángulo
            int numParticles = 1;
            for (int j = 0; j < numParticles; j++) {
                if (explosionType == 0) {
                    particles.push_back(new CircularExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else if (explosionType == 1) {
                    particles.push_back(new RandomExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else if (explosionType == 3) {
                    particles.push_back(new TriangleExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
                else {
                    particles.push_back(new StarExplosion(particles[i]->getPosition(), particles[i]->getColor()));
                }
            }
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
        else if (particles[i]->isDead()) {
            delete particles[i];
            particles.erase(particles.begin() + i);
        }
    }
}

// --------------------------------------------------------------
void ofApp::draw() {
    for (int i = 0; i < particles.size(); i++) {
        particles[i]->draw();
    }
}

// --------------------------------------------------------------
void ofApp::createRisingParticle() {
    // Genera una RisingParticle cerca del centro inferior (con variación horizontal)
    float minX = ofGetWidth() * 0.35;
    float maxX = ofGetWidth() * 0.65;
    float spawnX = ofRandom(minX, maxX);
    glm::vec2 pos(spawnX, ofGetHeight());
    // La partícula apunta hacia un objetivo en la parte superior central
    glm::vec2 target(ofGetWidth() / 2 + ofRandom(-300, 300), ofGetHeight() * 0.10 + ofRandom(-30, 30));
    glm::vec2 direction = glm::normalize(target - pos);
    // Velocidad ajustada para recorrer una mayor distancia
    glm::vec2 vel = direction * ofRandom(250, 350);
    ofColor col;
    col.setHsb(ofRandom(255), 220, 255);
    float lifetime = ofRandom(1.5, 3.5); // Tiempo de vida antes de explotar
    particles.push_back(new RisingParticle(pos, vel, col, lifetime));
}

void ofApp::createPulsingCubeParticle() {
    float posX = ofRandom(100, ofGetWidth() - 100);
    float posY = ofRandom(100, ofGetHeight() - 100);
    glm::vec3 pos(posX, posY, 0);

    ofColor col;
    col.setHsb(ofRandom(255), 180, 255, 200);

    float lifetime = ofRandom(1.5, 4);

    particles.push_back(new PulsingCubeParticle(pos, col));
}

void ofApp::createMouseParticle(int x, int y) {
    glm::vec2 pos(x, y);

    ofColor col;
    col.setHsb(ofRandom(255), 200, 255, 200);
    float lifetime = ofRandom(1.0, 2.0);

    particles.push_back(new MouseParticle(pos, col, lifetime));
}

// --------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
    //createRisingParticle();
}

// --------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == ' ') {
        for (int i = 0; i < 1000; i++) {
            createRisingParticle();
        }
    }
    if (key == 'a') {
        createPulsingCubeParticle();
    }
    if (key == 's') {
        ofSaveScreen("screenshot_" + ofToString(ofGetFrameNum()) + ".png");
    }
    if (key == 'b') {
        for (int i = 0; i < particles.size(); i++) {
            particles[i]->forceExplode();
        }
    }
}

//--------------------------------------------------------------
void ofApp::mouseDragged(int x, int y, int button) {
    // crear partículas mientras se arrastra el mouse
    if (button == OF_MOUSE_BUTTON_LEFT) {
        createMouseParticle(x, y);
    }
}
// --------------------------------------------------------------
ofApp::~ofApp() {
    for (int i = 0; i < particles.size(); i++) {
        delete particles[i];
    }
    particles.clear();
}
```
  
🌱 **¿Cómo y por qué de la implementación de los conceptos de encapsulamiento, herencia y polimorfismo en tu código?**
> ⭐ Cada una de las partículas tienen sus métodos protected y sus métodos public (menos las de explosión, que solo tienen public... y la de offApp, que tiene 3 métodos privados). Esos atributos solamente pueden ser modificados a través del constructor y los métodos para evitar que se redibujen las figuras incorrectamente al ser modificadas de forma indebida. El protected permite a todas las subclases acceder a esos atributos, pero igual está protegido desde afuera. Para las de explosión, creo que no es necesario por la vida súper cortica de ellas, aparte de que en el código no tenemos subclases de cada forma de explosión (solamente tenemos las distintas figuritas).  
> 🌟 Para la herencia, estoy utilizando una superclase de Particle y ExplosionParticle que definen los comportamientos y atributos de las demás partículas. Me ahorra andar repitiendo código.  
> ✨ Polimorfismo lo apliqué al modificar la manera en la que las partículas explotaban, cómo se actualizaban los datos y cómo se dibujaban. Un ejemplo podría ser el método forceExplode, donde al llamarlo para TODAS las partículas, solo una de ellas (el cubo) tenía código definido que la hacía explotar. Otra es en el draw, que algunas veces se dibuja un círcula, otras un cubo, otras un triángulo... en algunos updates se actualiza la posición, en otras rotación...  

🌿 **Explica cómo verificaste que cada una de las extensiones funciona correctamente, muestra capturas de pantalla del depurador donde evidencias lo anterior, en particular el polimorfismo en tiempo de ejecución.**
Ya había mencionado algunas cosas, como lo de modificar el número de partículas de explosión y fijarlo siempre en triángulo... pero voy más en detalle :P  
> Primero, me aseguré de que no pudieran aparecer más partículas que las que YO agregué. En el método de `mousePressed` quité que spawneara partículas tipo rising, porque eso haría conflicto con mi partícula de `mouseDragged`. Así, me quedó que la partícula de tipo rising solamente spawnea al presionar espacio y al inicio cuando la llamo manualmente.  
> Segundo, modifiqué la partícula rising para que siempre naciera muerta. Así, cada que yo presiono espacio, es una forma segura de revisar que la explosión en forma de tríangulo se dibuje y llame correctamente. Un plus es que como salen tantas, me deja ver cómo se vería más o menos la explosión de triangulitos con muchas más instancias.  
> Después, agregué al inicio que se spawneara una partícula de cubito, una de mouse y una de rising. Como la de rising nace muerta, entonces al poner un breakpoint después de draw, este se llama el primer frame y veo en la consola solamente: partícula de cubo, partícula de mouse, partícula de triangulito (que era la rising estallada). Esto me permite revisar la herencia, que se instancien correctamente, su posición en la memoria, etc...
<img width="907" height="659" alt="image" src="https://github.com/user-attachments/assets/b3937ff3-33fd-43bb-b646-dcd28e123e4b" />
<img width="1013" height="761" alt="image" src="https://github.com/user-attachments/assets/66215ba2-e866-49ea-8801-00118ac966e0" />
  
(foto de la consola y la pantalla en el frame inicial)  


> Cuando estaba programando el cubito, usé de referencia uno de los proyectos de muestra (el ofBoxExample). Ahí vi que estaban usando lo de push/pop matrix para dibujar los cubos, pero no entendía qué hacían? entonces lo borré de mi código a ver exactamente qué dañaba. Ahí ví que todas las partículas que antes se dibujaban bien, ahora tenían desplazamientos raros... entonces me fui a la docu a buscar para qué servía. Ya entendiéndolo, lo volví a agregar y todo funcionó bien. Después noté que también lo habías usado para las partículas de estrella, porque ahí también usabas el ofTranslate.

<img width="989" height="747" alt="image" src="https://github.com/user-attachments/assets/337d16a7-055b-4b00-8d65-dc8a9e36061f" />
<img width="986" height="743" alt="image" src="https://github.com/user-attachments/assets/0dc7daa2-8428-4c04-b871-dc85c242f00c" />
<img width="985" height="737" alt="image" src="https://github.com/user-attachments/assets/07f9365f-e398-4589-9651-bffe184ebefc" />
  
(fotos de cómo se ve con el push/pop matrix vs sin agregarlo. Literalmente es como que todo va dando vuelticas respecto al centro del primer cubito)  

> Por último, para demostrar lo del polimorfirmo en tiempo de ejecución, tomé esto:

<img width="925" height="514" alt="image" src="https://github.com/user-attachments/assets/157fa26a-974b-44b1-9f72-dc8f536395d8" />
  
> Donde se puede ver claramente que, para la partícula de triángulo, el update que se llama es el de ExplosionParticle directamente porque NO fue modificado... pero como el draw es único a sí mismo, entonces se llama específicamente el de TriangleExplosion. Por otro lado, como en la partícula de Mouse ambos fueron modificados, entonces en ambos métodos se llama MouseParticle::(método) :)
> Sobretodo en la partícula del triángulo es que se puede evidenciar más, porque ahí el scope resolution agarra métodos de su jerarquía entera.

> El resto del proceso fue simplemente darle play y confirmar que efectivamente todo me estaba funcionando correctamente.  

___ 

## 4.  **Consolidación, autoevaluación y cierre:**
1. **Mi nota propuesta:** 5 😼

2. **Justificación general:** siento que, aunque seguí el camino guiado con las preguntas que tú planteaste, no me quedé simplemente en la parte superficial de tomar capturas de la memoria, responder con lo teórico y ya está. Mi proceso a la hora de resolver las actividades es no hacer nada que no entienda completamente. Yo no hago copy-paste de tu código, no me conformo con saber que funciona y eso es suficiente, sino que busco el por qué exactamente. En el proceso de analizar la memoria identifiqué el scope resolution y su función, en el experimento individual busqué por qué no había métodos tipo abstract y cómo se implementa en la herencia que un método sea obligatorio, y en la fase de apply me salí de mi zona de comfort para investigar cómo implementar los objetos 3D y qué implicaba ese proceso. Además, no busco el camino de fácil de utilizar IA para que me haga los procedimientos... todo lo investigo por mi cuenta, todo lo pruebo yo misma, y todo lo intento comprender a punta de quitar/poner código y analizar los cambios hasta entender qué aporta al programa completo en general. Diría que me esforcé lo suficiente como para merecer la nota (o eso quiero creer) :D  

3. **Mapeo de evidencias según la rúbrica:**

| Criterio | Autoevaluación | Justificación / Evidencias |
|----------|----------------|----------------------------|
| Profundidad de la Indagación | Excelente | Como mencioné en mi justificación general, siento que realicé una buena investigación. Cada detalle chiquito, símbolo o método llamado que no comprendía, lo investigué hasta comprenderlo y sentirme capaz de explicarlo. Además, no me quedé simplemente con los dibujos 2D que hemos aprendido, sino que realicé por mi propia cuenta la indagación sobre cómo se implementaría una figura tridimensional y lo que eso implica. |
| Calidad de la Experimentación | Excelente | Considero que los experimentos que realicé me permitieron entender mucho mejor la implementación de la herencia y todo lo que sucede al implementarlo. En el experimento de los personajes, logré entender qué era el scope resolution, por qué en el algunos casos el scope resolution apuntaba a la clase individual, otras veces a su superclase, cuándo cambiaba la dirección de memoria del método, cuándo se compartía entre distintas subclases, cuándo un método debía ser implementado y modificado obligatoriamente, cómo implementar un método como el abstract en C++, etc. Me permitió, de una manera eficaz y precisa, confirmar las ideas que ya tenía sobre su funcionamiento y llenar los vacíos que me quedaban sobre el cambio entre lenguajes. Ejemplo del profe: como en la [captura1](#captura1) |
| Análisis y Reflexión | Excelente | Mi proceso de pensamiento siempre fue intentar identificar por mi cuenta qué rol tiene lo que estoy investigando, ver qué cambia si no lo implemento, ver qué arregla al volver a ponerlo, y por último buscar en internet la respuesta técnica. Me permite realmente darme la oportunidad de analizar y poner a prueba mis conocimientos en lugar de simplemente encontrar la solución en dos segundos. Siento que, especialmente en el experimento de los personajes, pude mostrar mi proceso de pensamiento y resolución de problemas. Se evidencia también en la forma en la que realicé las modificaciones al código de las partículas, realizando cambios mínimos que me garantizaran probar el programa de la forma más eficaz. Todo lo que hice fue premeditado y analizado. |
| Apropiación y Articulación de Conceptos | Excelente | Diría que en mi bitácora se puede evidenciar mi comprensión de todos los temas. Como mencioné, yo nunca implemento nada que no entienda. Todo lo que escribí, todo lo que programé, todo lo que utilicé... es porque entiendo realmente qué hace, qué aporta y qué se daña si no está ahí. Creo que es claro que comprendo la temática, evidenciado como ejemplo en el hecho de que fui capaz de transferir mis conocimientos desde las figuras 2d que hemos estado utilizando al código de la partícula 3D. | 
