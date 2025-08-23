# Unidad 3


## 🤔 Fase: Reflect

### 📝Actividad 11

🌱 **Explica con tus propias palabras qué es el stack y qué es el heap en C++.**  
> `Stack:` es la parte de la memoria que se encarga de almacenar datos con un ciclo de vida limitado a la función/método donde se encuentran. Son inicializados al momento de entrar a su método correspondiente, y al salir de este, son eliminadas de la memoria. Ahí se almacenan los parámetros, variables creadas en el main...  
> `Heap:` es una sección de la memoria que se encarga de contener todo lo definido por asignación de memoria dinámica. Para almacenar algo en él, se hace uso de palabras como `new`. Su memoria no se elimina automáticamente al salir de la función como en el stack, por lo que es necesario hacerlo de manera manual con la palabra `delete`. De lo contrario, puede provocar un memory leak.    

🌿 **Describe las tres formas de pasar parámetros a una función en C++ (valor, referencia y puntero). Para cada una, explica qué sucede en memoria y cuándo usarías cada método.**  
> `Valor:` se crea una copia de la variable original en el stack que se borra después de salir de la función donde se encuentra. Los cambios dentro de la función no la afectan. Lo usaría para cálculos chiquitos donde quiero mantener protegida la original.  
> `Referencia:` es como un "alias" en el stack para la variable original. Modifica su valor. Lo utilizaría para cambios de atributos como nombres y cosas de ese estilo.   
> `Puntero:` es una referencia al punto de la memoria donde se encuentra almaceanda la variable, que también permite editar su valor original. Lo utilizaría para arrays.  

🌼 **¿Qué diferencia hay entre una variable local, una variable global y una variable local estática? ¿En qué segmento del mapa de memoria se almacena cada una?**  
> `Variable local:` se crea en el stack cuando entra a la función y se destruye al salir. No se puede usar fuera de ella.   
> `Variable global:` se guarda en la sección global/static y se puede acceder a ella desde cualquier parte del código.   
> `Variable local estática:` también se guarda dentro de global/static, pero solamente se puede acceder a ella dentro de la función donde se encuentra. Se inicializa una sola vez la primera vez que se corre el código y su valor se comparte entre instancias de la clase.  

🌻 **Explica qué es un objeto en C++ desde la perspectiva de memoria. ¿Dónde se almacenan los miembros de instancia y dónde los miembros estáticos?**  
> Es una instancia de una clase con parámetros y variables que ocupan un espacio específico de memoria dependiendo de cómo fueron inicializados. Se almacenan en el stack si fueron creados localmente, en el Heap si se crearon usando `new`, y en la sección global/estática si son estáticos.  
___
Errores:   
1. Usa asignación dinámica de memoria para inicializar `armas = new int[3]`. Como es memoria dinámica y en el código jamás se usa `delete`, cada vez que se corre el programa está comiendo más y más memoria.  
2. No tiene un destructor para eliminar las intancias de la memoria.
3. Al usar int* armas se crea un puntero hacia el array. Cuando hace una copia enemigo, no copia el array sino la dirección de la memoria, por lo que ambos comparten el mismo array armas. Si se modifica o elimina en uno, en el otro también.
  
totalEnemigos mostraría 10, porque se ejecuta 2 veces, cada uno creando 5 instancias.  
Solución:  
```program.cpp
#include <iostream>
using namespace std;

class Enemigo {
public:
    static int totalEnemigos;
    int vida;
    int armas[3] = {0,0,0},

    Enemigo(int v) : vida(v) {
        totalEnemigos++;
        armas[0] = 10; armas[1] = 15; armas[2] = 20;
    }

    ~Personaje() {
        std::cout << "Destructor: Personaje(" << nombre << ") destruido." << std::endl;
    }
};

int Enemigo::totalEnemigos = 0;

void crearEscuadron() {
    for(int i = 0; i < 5; i++) {
        Enemigo soldado(100);
        soldado.vida -= 10;
    }
    cout << "Escuadrón creado. Total enemigos: " << Enemigo::totalEnemigos << endl;
}

int main() {
    crearEscuadron();
    crearEscuadron();
    return 0;
}
```
___

🌱 **De todos los conceptos que exploraste en esta unidad (stack vs heap, paso de parámetros, ciclo de vida de objetos, etc.), ¿Cuál consideras que es el más crítico para evitar errores en programas reales? ¿Por qué?**  
> La parte de liberar la memoria del heap, porque es algo fácil de olvidar y puede causar MUCHOS problemas al ocupar progresivamente más y más espacio innecesario.   

🌿 **¿Cómo cambió tu comprensión sobre lo que realmente es un “objeto” después de comparar C++ con C#? ¿Qué implicaciones prácticas tiene esta diferencia?**  
> Me sorprendió bastante. En ningún momento en los cursos pasados nos explicaron que realmente no estábamos trabajando directamente con objetos. Ahora estoy pensando en toda la cantidad de programas que escribirmos donde nunca usamos destructores ni liberamos la memoria, y no entiendo por qué jamás nadie lo mencionó. Creo que en C++ hay que ser mucho más cuidadosos con ese tema.   

🌼 **Si tuvieras que explicar a un compañero de semestres anteriores por qué es importante entender la gestión de memoria en programación, ¿Qué le dirías en máximo 3 oraciones?**  
> Que si no logran gestionar bien la memoria, esos programas no les van a correr bien en el portátil que traen a la universidad y Unity les va a tirar miles de errores amarillos por memory leaks. Si no aprenden a manejar eso, no hay diferencia entre contratarlos a ellos o pedirle a chatgpt que haga el programa... es el mismo nivel de riesgo en el código (o hasta menos).  



