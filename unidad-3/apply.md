# Unidad 3


## 🛠 Fase: Apply
# 📝 Actividad 06

🌱 **¿Cuál es la diferencia entre un constructor y un destructor en C++?**  
> El contructor instancia un objeto de una clase específica. Recibe los parámetros que asignamos. El destructor no recibe parámetros, simplemente elimina la instancia el objeto.    

🌿 **¿Cuál es la diferencia entre un objeto y una clase en C++?**  
> Una clase es el conjunto de parámetros, atributos y funciones que definen a un objeto y su comportamiento. El objeto es una instancia de esa clase con los atributos mencionados, ocupando un espacio de memoria asignado.   

🌼 **¿Qué diferencia notas entre el objeto Punto en C++ y C#?**  
> En el de C++, no es necesario llamar al destructor... una vez se ejecuta el contructor y la función imprimir, automáticamente se destruye. En C#, esto no sucede, por lo que el destructor nunca se llama.  

🌻 **¿Qué es p en C++ y qué es p en C#? (en uno de ellos p es un objeto y en el otro es una referencia a un objeto).**  
> Creo que en C++ es un objeto y en C# es una referencia a un objeto. 

🌱 **¿En qué parte de memoria se almacena p en C++ y en C#?**  
> Creo que en C++ está en el stack, porque el destructor se ejecuta po sí solo... y en C# quizás es heap?

___

# 📝 Actividad 07

En el stack: `0x000000B11418FB58`,  `0x0000000275B5FA68`, `0x000000FB1DAFF5A8`...    
En el heap: `0x000000B11418FB78`, `0x0000000C2036F848`, `0x000000886E11F508`, `0x0000000275B5FA88`...    
No entiendo por qué, pero cada vez que volvía a ejecutar el programa, la dirección de memoria de pHeap y pStack cambiaba.    

> Nota: el formato para instanciar el objeto en el heap es MUY similar al de C#, por lo que creo que, efectivamente, en C# es también una referencia a un objeto.

Los objetos creados en el stack se eliminan automáticamente cuando se sale del método. Los objetos creados en el heap tienen que declararse manualmente con `new` y borrarse con `delete`, o se quedan ocupando la memoria.   
  
**pStack:** Objeto  
**pHeap:** Referencia a un objeto (al objeto Punto en el Heap)  

___

# 📝 Actividad 08

🌱 **¿Qué ocurre después de llamar a la función cambiarNombre? ¿Por qué aparece el mensaje Destructor: Punto cambiado(70, 80) destruido.? ¿Por qué original sigue existiendo luego de llamar cambiarNombre? ¿En qué parte del mapa de memoria se encuentra original y en qué parte se encuentra p? ¿Son el mismo objeto?**  
> cambiarNombre está creando una copia del punto P en el stack, no es una referencia directa. Cuando cambia el nombre, sólo lo cambia para la variable que está dentro del método. Cuando sale del método, como ya vimos que sucede en el stack en c++, se destruye automáticamente... pero lo que está destruyendo es la copia, no el original. El punto original no solo sigue instanciado, sino que también conserva su nombre original. Ambos están en el stack, pero son objetos distintos.  

🌿 **Modifica la función cambiarNombre. ¿Qué ocurre ahora? ¿Por qué?**  
> Ahora sí cambia el nombre del objeto. Ya no se está creando una copia del punto, sino que se está haciendo una referencia a él con un apodo. Como ya el objeto no vive solamente dentro de el método de cambiarNombre, el destructor no se ejecuta hasta el final. No se crea una copia, es el mismo objeto con un atributo cambiado.  

🌼 **Modifica ahora a cambiarNombre y a main de la siguiente manera. ¿Qué ocurre ahora? ¿Por qué?**  
> También funciona, pero aquí se está usando un puntero. Modifica también el valor original en lugar de crear una copia, entonces también se ejecuta el destructor solamente al final.  

___

# 📝 Actividad 09

🌱 **¿En dónde está almacenado el miembro valor y el miembro total de la clase Contador?**  
> `Valor` está en el stack, `total` está en globales/estáticas.  

🌿 **¿Qué puedes concluir de los miembros estáticos y de instancia de una clase en C++? ¿Cómo se gestionan en memoria?**  
> Los miembros estáticos se comparten entre todos los objetos, mientras que los de instancia tienen valores que pueden variar de instancia a instancia. Los estáticos se almacenan en la zona de globales/estáticos, y los de instancia en el stack. 

🌼 **En el programa, en qué segmento de memoria se están almacenando c1, c2, c3 y Contador::total?**  
> c1 y c2 se están almacenando en el stack, pero la forma en la que está inicializada c3 (usando new) lo crea en la sección del Heap.   

___

# 📝 Actividad integradora de aplicación
**Errores:**  
1. Utiliza asignación dinámica de memoria para definir que `estadisticas = new int[3]`. Al ser memoria dinámica (lo cuál identifico por la palabra `new`), el array queda almacenado en el Heap y luego **nunca lo borra**. La consecuencia (creo) sería un memory leak. Cada vez que se llama el constructor, se come más memoria. En su lugar, podría simplemente escribir `int estadisticas[3] = { 0,0,0 };` desde un inicio para instanciarlo en el stack (se recomienda inicializar con valores default porque lo hace más predecible y evita errores al intentar acceder a un índice del array que no esté definidido).
2. Creo que con `int* estadísticas` lo que está haciendo es crear un puntero hacia el array estadísticas. Cuando hace una copia al objeto heroe, no está haciendo una copia del array... sino que está tomando la misma dirección a la que apunta ese puntero. Eso haría que ambos objetos, aunque sean dos instancias distintas, compartan el mismo array de estadísticas. Si se hace un cambio en uno, se cambiaría también en el otro. Y si yo borro una de las instancias, también le eliminaría el array al que quede... lo cuál podría hacer que cuando yo intente referenciar ese array, me tire un error.

  
Corrección:  
```program.cpp
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int estadisticas[3] = { 0,0,0 }; //AQUÍ EL CAMBIO QUE HICE :D

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    ~Personaje() //para poder verlo
    {
        std::cout << "Destructor: Personaje(" <<nombre<< ") destruido." << std::endl;
    }

    void imprimir() {
        std::cout << "Personaje " << nombre
            << " [Vida: " << estadisticas[0]
            << ", ATK: " << estadisticas[1]
            << ", DEF: " << estadisticas[2]
            << "]" << std::endl;
    }
};

void simularEncuentro() {
    std::cout << "\n--- Iniciando encuentro ---" << std::endl;
    Personaje heroe("Aragorn", 100, 20, 15);

    Personaje copiaHeroe = heroe;
    copiaHeroe.nombre = "Copia de Aragorn";

    heroe.imprimir();
    copiaHeroe.imprimir();

    std::cout << "Saliendo del encuentro..." << std::endl;
}

int main() {
    simularEncuentro();
    std::cout << "\nSimulación terminada." << std::endl;
    return 0;
}
```

Funciona porque ahora:
- El array se está creando en el stack (lo que significa que se va a borrar automáticamente cuando termine su ciclo de vida).  
- Empieza con valores default que evitan referencias a valores no definidos.  
- Al crear la copia de Aragorn, ya no está tomando la dirección del mismo array... sino que está copiando un array nuevo con las mismas estadísticas que el original. Si se borra uno de los dos, el otro sigue funcionando.  

