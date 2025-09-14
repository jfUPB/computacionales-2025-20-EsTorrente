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
    
___

## Actividad 02

> 🌱 El programa tiene una superclase de partícula, y unas subclases de partículas con distintos comportamientos. Tiene varios métodos de tipo virtual, lo que significa que cada subclase puede decidir si modificarlos o mantenerlos igual en su implementación individual.  

> 🌿 Para  RisingParticle (subclase de Particle), creo que está creando una partícula con un tiempo de vida definido que va subiendo en la pantalla de a poquito. El programa cuenta cuánto tiempo lleva después de haber spawneado. Si el tiempo de vida ya llegó al máximo, o alcanzó la altura definida como threshold, entonces la partícula explota.  

> 🌼 En ExplosionParticle (subclase de Particle), es casi el mismo concepto. Aquí se está tomando el tiempo que lleva la partícula de explosión viva. Si el tiempo supera la vida máxima, entonces se dice que la partícula muere. La transparencia de la partícula se va actualizando, utilizando ofMap() para definir que al inicio de la vida tendrá la saturación al full, y cuando alcance la vida máxima será 0.  

> 🌻 Para CircularExplosion (subclase de ExplosionParticle), se está definidiendo un patrón circular de la explosión usando senos y cosenos. Para RandomExplosion (subclase de ExplosionParticle), creo que simplemente se está definiendo una dirección random para estallar. Sin embargo, en el override de draw, veo que ya no se está dibujando la partícula con forma de círculo sino de rectángulo. En StarExplosion (subclase de ExplosionParticle), creo que se está dibujando la partícula con forma de estrella en la que el radio interno y externo aumentan con el tiempo.   

> 🌱 Luego, en ofApp.cpp, se están actualizando todas las partículas en cada frame. Usando el método definido en la clase Particle para ExplosionParticle y RisingParticle, si se cumple la condición de que deba estallar, escoge un patrón random de las 3 opciones. Le asigna un número random de partículas de la explosión, las instancia y las va borrando (tanto la original como las del efecto).  

> 🌿 Creo que las partículas rising se están instanciando al hacer clic o presionar espacio. Si se presiona la S, se guarda un screenshot del programa.

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
🌿 **¿Qué relación existe entre los métodos virtuales y el polimorfismo?**  
> Los métodos virtuales son lo que permite a las subclases heredar métodos y adaptarlos a sus necesidades individuales. Se junta con el cosito de los :: (ya se me olvidó el nombre D:) para definir cuál es el método específico que se debe llamar en cada clase.  
___ 

## 3.  **Registro de exploración:** 
> Aquí documentas cada ciclo de pregunta -> hipótesis -> experimento -> hallazgo -> reflexión.
> Debe ser rico en evidencia visual (código, capturas del depurador con anotaciones, diagramas).

## 4.  **Consolidación, autoevaluación y cierre:**
