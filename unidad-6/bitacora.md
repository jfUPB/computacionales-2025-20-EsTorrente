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

<a name="AnalisisPrograma"></a>
🌻 **¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.**
> En el estado de stop, la velocidad es 0 (no hay movimiento). En el estado normal, se le asigna una velocidad random que se le suma a su posición. Para repelerla y atraerla, me imagino que la posición de la partícula está siendo sumada o restada por la posición del mouse... al mismo tiempo, creo que la velocidad se estaría multiplicando por el valor de una fuerza que actúa sobre ella. Veo que las partículas están cambiando de estados en base a una notificación que les envía un evento. Dependiendo de la notificación que les llegue, se settean en un estado... y cada uno de esos estados tiene un método que modifica los valores de los atributos en TOOODAS las partículas que están instanciadas.  

___

### 📝 Actividad 2
🌱 **Explica con tus propias palabras el propósito del patrón Observer. ¿Qué problema resuelve?**
> El patrón Observer provoca que las clases dependan menos entre ellas, lo que es bueno porque significa menor acoplamiento. Además, como mencionaste en la clase, permite que muchas personas trabajen en sus clases separadas sin tener que esperar a recibir los avances de los demás, sino que todo puede adelantarse y simplemente ponerse de acuerdo en la interfaz del Observer.  

<a name="Diagrama02"></a>
🌿 **Dibuja un diagrama que muestre la relación entre Subject, Observer, ofApp y Particle en el caso de estudio, indicando quién es el Sujeto y quiénes los Observadores.**
<img width="1162" height="660" alt="image" src="https://github.com/user-attachments/assets/fa257073-6a83-4767-bed7-31e3b4523cb6" />  
   
🌼 **Construye un diagrama de secuencia que muestre cómo funciona el patrón Observer al presionar una tecla.**  
<img width="978" height="829" alt="image" src="https://github.com/user-attachments/assets/c1596543-3fff-4834-8b7e-6293fbd939dd" />  

🌻 **¿Qué ventajas crees que ofrece usar el patrón Observer en esta aplicación en comparación con, por ejemplo, que ofApp::update recorriera todas las partículas y les dijera directamente que cambien su comportamiento basado en una variable global? Piensa en términos de acoplamiento y extensibilidad.**
> ofApp tendría que tener acceso a las variables internas de cada particle, estaría haciendo demasiadas tareas solita y se enreda si se quieren agregar comportamientos diferentes. Con el observer, el ofApp nada más manda notificación y las partículas ven cómo reaccionan por su cuenta. Cada clase queda con poquitas responsabilidades, y además, el sistema de notificaciones es útil para otras funciones si se quieren implementar en el futuro.

___

### 📝 Actividad 3
<a name="FactoryProposito"></a>
🌱 **Explica con tus propias palabras el propósito del patrón Factory Method (o Simple Factory, en este caso). ¿Qué problema principal aborda en la creación de objetos?**
> Simplifica mucho el proceso de creación de objetos. No deja códigos new en todas partes, sino que encapsula todo en un método que se encargue de separar las distintas variaciones posibles y cómo instanciarlas. El problema principal que soluciona es que si hay que hacer modificaciones, arreglar código, hacer debug o agregar un tipo nuevo de partícula, es MUCHÍSIMO más fácil sólo revisar un método en una clase, que irse a buscar un montón de métodos chiquitos súper parecidos en miles de clases.  
  
🌿 **¿Qué ventajas aporta el uso de ParticleFactory en ofApp::setup en comparación con instanciar y configurar las partículas directamente allí? Piensa en términos de organización del código (SRP - Single Responsibility Principle), legibilidad y facilidad para añadir nuevos tipos de partículas en el futuro.**
> Le permite al ofApp seguirse concentrando en una sola función: recibir inputs y mandar notificaciones, fin. Es bueno que en un código, cada método y cada clase tenga funciones muy específicas. ParticleFactory tiene solo una función: instanciar los distintos tipos de partículas, fin. Gracias a eso, como mencioné antes, es muchísimo más fácil realizar modificaciones y adiciones al código.  

<a name="BlackHole"></a>
🌼 **Imagina que quieres añadir un nuevo tipo de partícula llamada "black_hole" que tiene tamaño grande, color negro y velocidad muy lenta. Describe los pasos que necesitarías seguir para implementar esto utilizando la ParticleFactory existente. ¿Tendrías que modificar ofApp::setup? ¿Por qué sí o por qué no?**  
> Síp! para que en el setup le diga cuántas de esas partículas crear en el ParticleFactory. Es solamente agregar otro for donde se le indique la cantidad... pero lo de cambiar los atributos del tamaño, color y velocidad sería TODO en el ParticleFactory, ahí no se tiene que tocar el setup en absoluto. O sea, no tengo que cambiar nada de la lógica... solamente copi pastear y cambiar el nombre de la partícula.  

🌻 **El método createParticle en el ejemplo es estático. ¿Qué implicaciones (ventajas/desventajas) tiene esto comparado con tener una instancia de ParticleFactory y un método de instancia createParticle()?.**
> Lo bueno es que no toca instanciar para nada un ParticleFactory, sino que se puede llamar de una al método. Lo malo es que no se le puede hacer override, lo que significa que no se puede meter polimorfismo, porque ese método lo comparte toda la clase... no cada instancia.

___

### 📝 Actividad 4
🌱 **Explica con tus propias palabras el propósito del patrón State. ¿Cuándo es útil aplicarlo?**
> En vez de tener un montón de ifs o switchs que checkeen un montón de estados posibles, permite encapsularlos todos. Se implementan cuando un objeto tiene que hacer cambios internos tan drásticos que hasta parecen una clase diferente. También te da la capacidad de definir transiciones entre los estados (al entrar y salir de ellos).   

<a name="Diagrama04"></a>
🌿 **Dibuja un diagrama de estados simple para la clase Particle. Muestra los diferentes estados (Normal, Attract, Repel, Stop) como nodos y las transiciones entre ellos como flechas etiquetadas con el evento que las causa (p. ej., la tecla presionada: ‘n’, ‘a’, ‘r’, ‘s’).**  
<img width="1086" height="450" alt="image" src="https://github.com/user-attachments/assets/24dec6db-17e9-482f-9af1-028e105f50e3" />  

<a name="VentajasState"></a>
🌼 **Describe las ventajas de usar el patrón State en Particle en lugar de tener un miembro std::string estadoActual y usar un gran if/else if/else o switch dentro de Particle::update() para cambiar el comportamiento. Piensa en cohesión, extensibilidad (añadir nuevos estados) y el Principio Abierto/Cerrado (Open/Closed Principle).**  
> Otra vez volvemos a que cada clase debe tener funciones muy específicas, todo debe tener el menor grado de acoplamiento posible, no deben depender unas de otras, y NO SE DEBE TENER QUE ABRIR EL PARTICLE PARA MODIFICARLO!! entonces, tener un montón de switch o ifs dentro de esa clase probocaría que:  
> 1. Tocara abrirla para quitar/agregar estados, lo cuál va en contra del principio.  
> 2. Particle tenga muchísimas tareas y checks y cosas por estar revisando.  
> 3. el código sea maluco de leer.  
> Usar el patrón state hace que todo sea más bonito, modular, fácil de modificar y siga los principios de POO.  

🌻 **¿Qué responsabilidad tienen los métodos onEnter y onExit en el patrón State? Proporciona un ejemplo de por qué podrían ser útiles (incluso si no se usan mucho en todos los estados de este caso de estudio). Por ejemplo, ¿Qué podrías hacer en onEnter para AttractState o en onExit para StopState?**
> Tienen la responsabilidad de preparar las partículas para los cambios entre estados. Si no se resetean o actualizan datos al entrar y salir de algunos estados, puede dañar el funcionamiento de los demás. También puede servir simplemente por estética, para agregar algún comportamiento que indique o suavice la transición. Por ejemplo, en el onEnter de AttractState, podría hacer que todas las bolitas cambien de color a uno mismo para simbolizar que son como una mente colmena... y para el onExit del stopState, podría hacer una animación chiquita donde cada partícula se hace un poquito más grande y después regresa a su tamaño original antes de retomar su movimiento, para que no se vea tan drástico el cambio de estar congelado a moverse. También podría servir para poner logs que permitan revisar esos cambios.  

___

### 📝 Apply

Mi idea era hacer una partícula rebelde que recibiera las notificaciones, pero decidiera hacer el total opuesto de lo que le pedimos. Para conseguirlo, modifiqué el onNotify de Particle:
```p.cpp
bool isRebel = (color == ofColor(255, 50, 50)); // identifica por color (racismo)

if (isRebel) {
    // hace lo contrario de las otras pq es rebelde >:T
    if (event == "attract") {
        setState(new RepelState());
    }
    else if (event == "repel") {
        setState(new AttractState());
    }
    else if (event == "stop") {
        setState(new NormalState());
    }
    else if (event == "normal") {
        setState(new StopState());
    }
}
else {
    //particulitas normales
    if (event == "attract") {
        setState(new AttractState());
    }
    else if (event == "repel") {
        setState(new RepelState());
    }
    else if (event == "stop") {
        setState(new StopState());
    }
    else if (event == "normal") {
        setState(new NormalState());
    }
}
```

🌱 `Patrón state:`  
> La partícula rebelde tiene un puntero a un objeto State (state). Dependiendo del evento recibido en onNotify, hace un setState(new AttractState()), setState(new RepelState()), etc. Cada estado define el comportamiento en su método update(). La diferencia está en que las rebeldes cambian a estados contrarios a los de las normales, lo que las hace exponencialmente más charritas. Así, la rebelde comparte la misma infraestructura de estados (NormalState, AttractState, RepelState, StopState), pero su lógica de transición es distinta gracias al código en onNotify. Esto demuestra que no tuve que crear estados nuevos, sino que reutilicé los existentes, pero con una lógica de transición distinta.  
  
🌿 `Patrón observer:`
> En ofApp::setup, cada partícula (incluyendo las rebeldes) se registra con addObserver(p). Cuando el usuario presiona una tecla (a, r, s, n), el ofApp llama a notify("evento"). Todas las partículas reciben la notificación en su método onNotify, incluyendo el rebelde. Con esto, la nueva partícula rebelde sigue siendo un Observer, pero con un comportamiento distinto al interpretar los eventos.
  
🌼 `Patrón factory:`
> Para la nueva partícula "rebel", agregué un caso en ParticleFactory de if (type == "rebel"). Dentro de ese caso le di características especiales: chiquita (1.0f a 2.0f para size), enojada (ofColor(255, 50, 50) rojo, que también permite identificarlas fácilmente), e hiperactiva (velocidad multiplicada (* 5.0f) para que se noten más rápidas). De esta forma, el código que usa la ParticleFactory no necesita saber cómo se construyen las rebeldes, sino que solo pide "rebel" y la fábrica se encarga de todo lo otro.
  
Con estas modificaciones logro demostrar lo versátil y fácil que es utilizar estos patrones. Literal sólo tuve que mover como unas 5 líneas de código para hacer una partícula que iba en contra de lo ya establecido, sin tener que mover en ningún momento NADA del ofApp.h ni la clase de partículas como tal. Todo es súper modular, súper eficaz y muy fácil de integrar en el caso de que varias personas estuviéramos trabajando juntas.

🌱 ofApp.h (lit no lo toqué en absoluto)
```p.cpp
#pragma once

#include "ofMain.h"
#include <string>
#include <vector>

class Observer {
public:
  virtual ~Observer() = default;
  virtual void onNotify(const std::string & event) = 0;
};

class Subject {
public:
  void addObserver(Observer * observer);
  void removeObserver(Observer * observer);

protected:
  void notify(const std::string & event);

private:
  std::vector<Observer *> observers;
};

class Particle;

class State {
public:
  virtual ~State() = default;
  virtual void update(Particle * particle) = 0;
  virtual void onEnter(Particle * particle) { }
  virtual void onExit(Particle * particle) { }
};

class Particle : public Observer {
public:
  Particle();
  ~Particle() override;

  Particle(const Particle &) = delete;
  Particle & operator=(const Particle &) = delete;

  void update();
  void draw();
  void onNotify(const std::string & event) override;

  void setState(State * newState);

  ofVec2f position;
  ofVec2f velocity;
  float size;
  ofColor color;

private:
  void keepInsideWindow();
  State * state;
};

class NormalState : public State {
public:
  void update(Particle * particle) override;
  void onEnter(Particle * particle) override;
};

class AttractState : public State {
public:
  void update(Particle * particle) override;
};

class RepelState : public State {
public:
  void update(Particle * particle) override;
};

class StopState : public State {
public:
  void update(Particle * particle) override;
};

class ParticleFactory {
public:
  static Particle * createParticle(const std::string & type);
};

class ofApp : public ofBaseApp, public Subject {
public:
  ~ofApp() override;
  void setup() override;
  void update() override;
  void draw() override;
  void keyPressed(int key) override;

private:
  std::vector<Particle *> particles;
};
```
  
🌿 ofApp.cpp
```p.cpp
#include "ofApp.h"
#include <algorithm>

void Subject::addObserver(Observer* observer) {
    if (!observer) return;
    if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
        observers.push_back(observer);
    }
}

void Subject::removeObserver(Observer* observer) {
    if (!observer) return;
    observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
}

void Subject::notify(const std::string& event) {
    for (Observer* observer : observers) {
        observer->onNotify(event);
    }
}

Particle::Particle()
    : state(nullptr) {
    position = ofVec2f(ofRandomWidth(), ofRandomHeight());
    velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
    size = ofRandom(2.0f, 5.0f);
    color = ofColor(255);

    state = new NormalState();
    state->onEnter(this);
}

Particle::~Particle() {
    if (state) {
        state->onExit(this);
        delete state;
        state = nullptr;
    }
}

void Particle::setState(State* newState) {
    if (state) {
        state->onExit(this);
        delete state;
    }
    state = newState;
    if (state) {
        state->onEnter(this);
    }
}

void Particle::update() {
    if (state) {
        state->update(this);
    }
    keepInsideWindow();
}

void Particle::draw() {
    ofPushStyle();
    ofSetColor(color);
    ofDrawCircle(position, size);
    ofPopStyle();
}

void Particle::onNotify(const std::string& event) {
    bool isRebel = (color == ofColor(255, 50, 50)); // identifica por color (racismo)

    if (isRebel) {
        // hace lo contrario de las otras pq es rebelde >:T
        if (event == "attract") {
            setState(new RepelState());
        }
        else if (event == "repel") {
            setState(new AttractState());
        }
        else if (event == "stop") {
            setState(new NormalState());
        }
        else if (event == "normal") {
            setState(new StopState());
        }
    }
    else {
        //particulitas normales
        if (event == "attract") {
            setState(new AttractState());
        }
        else if (event == "repel") {
            setState(new RepelState());
        }
        else if (event == "stop") {
            setState(new StopState());
        }
        else if (event == "normal") {
            setState(new NormalState());
        }
    }
}

void Particle::keepInsideWindow() {
    const float W = static_cast<float>(ofGetWidth());
    const float H = static_cast<float>(ofGetHeight());

    if (position.x < 0.0f) {
        position.x = 0.0f;
        velocity.x *= -1.0f;
    }
    else if (position.x > W) {
        position.x = W;
        velocity.x *= -1.0f;
    }
    if (position.y < 0.0f) {
        position.y = 0.0f;
        velocity.y *= -1.0f;
    }
    else if (position.y > H) {
        position.y = H;
        velocity.y *= -1.0f;
    }
}

void NormalState::onEnter(Particle* particle) {
    particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
}

void NormalState::update(Particle* particle) {
    particle->position += particle->velocity;
}

static void steer(Particle* particle, const ofVec2f& toward, float accel, float vmax, float posScale) {
    ofVec2f dir = toward - particle->position;
    float len = dir.length();
    if (len > 1e-6f) {
        dir /= len;
        particle->velocity += dir * accel;
    }
    particle->velocity.limit(vmax);
    particle->position += particle->velocity * posScale;
}

void AttractState::update(Particle* particle) {
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    steer(particle, mouse, /*accel*/ 0.05f, /*vmax*/ 3.0f, /*posScale*/ 0.2f);
}

void RepelState::update(Particle* particle) {
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    ofVec2f away = particle->position - mouse;
    float len = away.length();
    if (len > 1e-6f) {
        away /= len;
        particle->velocity += away * 0.05f;
    }
    particle->velocity.limit(3.0f);
    particle->position += particle->velocity * 0.2f;
}

void StopState::update(Particle* particle) {
    particle->velocity *= 0.80f;
    if (particle->velocity.lengthSquared() < 1e-4f) {
        particle->velocity.set(0.0f, 0.0f);
    }
    particle->position += particle->velocity;
}

Particle* ParticleFactory::createParticle(const std::string& type) {
    Particle* particle = new Particle();

    if (type == "star") {
        particle->size = ofRandom(2.0f, 4.0f);
        particle->color = ofColor(255, 0, 0);
    }
    else if (type == "shooting_star") {
        particle->size = ofRandom(3.0f, 6.0f);
        particle->color = ofColor(0, 255, 0);
        particle->velocity *= 3.0f;
    }
    else if (type == "planet") {
        particle->size = ofRandom(5.0f, 8.0f);
        particle->color = ofColor(0, 0, 255);
    }
    else if (type == "rebel") { // la mía :D
        particle->size = ofRandom(1.0f, 2.0f);
        particle->color = ofColor(255, 50, 50);
        particle->velocity *= 5.0f;
    }
    return particle;
}

ofApp::~ofApp() {
    for (Particle* p : particles) {
        removeObserver(p);
        delete p;
    }
    particles.clear();
}

void ofApp::setup() {
    ofBackground(0);
    particles.reserve(100 + 5 + 10);

    for (int i = 0; i < 100; ++i) {
        Particle* p = ParticleFactory::createParticle("star");
        particles.push_back(p);
        addObserver(p);
    }
    for (int i = 0; i < 5; ++i) {
        Particle* p = ParticleFactory::createParticle("shooting_star");
        particles.push_back(p);
        addObserver(p);
    }
    for (int i = 0; i < 10; ++i) {
        Particle* p = ParticleFactory::createParticle("planet");
        particles.push_back(p);
        addObserver(p);
    }
    for (int i = 0; i < 3; ++i) {
        Particle* p = ParticleFactory::createParticle("rebel");
        particles.push_back(p);
        addObserver(p);
    }
}

void ofApp::update() {
    for (Particle* p : particles) {
        p->update();
    }
}

void ofApp::draw() {
    for (Particle* p : particles) {
        p->draw();
    }
}

void ofApp::keyPressed(int key) {
    switch (key) {
    case 's':
        notify("stop");
        break;
    case 'a':
        notify("attract");
        break;
    case 'r':
        notify("repel");
        break;
    case 'n':
        notify("normal");
        break;
    default:
        break;
    }
}
```

___

### 📝 Autoevaluación

### 🌱 **Nota Propuesta: 5**


| Actividad | Evaluación | Justificación / Evidencias |
|-----------|------------|----------------------------|
| ⭐ 01 | Excelente | Considero que identifiqué claramente el [funcionamiento interno](#AnalisisPrograma) de presionar cada tecla ("a" atrae, "r" repele, "s" detiene, "n" normal), tomé capturas de pantalla representativas de cada estado y formulé hipótesis fundamentadas sobre el comportamiento interno. Logré analizar correctamente cómo la clase Particle se modifica mediante el factory para crear diferentes tipos de partículas, demostrando comprensión tanto del comportamiento observable como de la implementación que le sigue. |
| ⭐ 02 | Excelente | Comprendí el patrón Observer y su implementación en el código. Creé [diagramas](#Diagrama02) claros que ilustran las relaciones entre Subject, Observer, ofApp y Particle, y desarrollé un diagrama detallado que explica el flujo de notificaciones. Mi análisis sobre las ventajas del patrón (bajo acoplamiento, alta extensibilidad) demuestra que internalicé bien los conceptos teóricos y los relacioné con el caso práctico. Creo que identifiqué correctamente todos los componentes del patrón y su interacción en el código. |
| ⭐ 03 | Excelente | Analicé críticamente la implementación del Factory Method en el código. En mi bitácora, expliqué con claridad el [propósito del patrón](#FactoryProposito) y sus ventajas respecto al principio de responsabilidad única. Mi respuesta sobre cómo añadir una nueva partícula ["black_hole"](#BlackHole) muestra comprensión práctica del patrón: identificué que solo sería necesario modificar ParticleFactory, no ofApp::setup. Además, evalué las implicaciones de usar un método estático versus de instancia, demostrando capacidad de análisis técnico. |
| ⭐ 04 | Excelente | Demostré dominio completo del patrón State mediante análisis teórico y práctico. Creé un [diagrama](#Diagrama04) de estados preciso que muestra todas las transiciones posibles, y analicé [ventajas específicas](#VentajasState) como mejor cohesión, adherencia al principio abierto/cerrado y mayor escalabilidad. Mi explicación sobre los métodos onEnter y onExit incluye ejemplos creativos y prácticos que van más allá del caso de estudio, mostrando capacidad de aplicar el concepto fuera del ejemplo. |
| ⭐ 05 | Excelente | Implementé una modificación creativa al añadir partículas "rebeldes". Como se evidencia en el código completo que incluí en la bitácora, demostré dominio práctico de los tres patrones: **Factory** (añadí caso "rebel" en ParticleFactory), **Observer** (mantuve el registro de observadores) y **State** (modifiqué la lógica de transición en onNotify). Reutilicé los estados existentes pero con lógica invertida, mostrando comprensión profunda de la arquitectura y demostrando la ventaja de trabajar modularmente. |

En cada actividad, analicé ventajas y desventajas, consideré alternativas de implementación y reflexioné sobre principios de diseño. Considero que merezco el 5.0 por haber completado todas las actividades, demostrado comprensión profunda de los tres patrones de diseño, y aplicado los conceptos de manera creativa.
