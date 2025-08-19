# Unidad 3


## 🛠 Fase: Apply
# 📝 Actividad 06

🌱 **¿Cuál es la diferencia entre un constructor y un destructor en C++?**  
> El contructor instancia un objeto de una clase específica. Recibe los parámetros que asignamos. El destructor no recibe parámetros, simplemente elimina la instancia el objeto.    

🌿 **¿Cuál es la diferencia entre un objeto y una clase en C++?**  
> Una clase es el conjunto de parámetros, atributos y funciones que definen a un objeto y su comportamiento. El objeto es un espacio de la memoria dedicado a instanciar una versión de esa clase con los atributos mencionados.  

🌼 **¿Qué diferencia notas entre el objeto Punto en C++ y C#?**  
> En el de C++, no es necesario llamar al destructor... una vez se ejecuta el contructor y la función imprimir, automáticamente se destruye. En C#, esto no sucede, por lo que el destructor nunca se llama.  

🌻 **¿Qué es p en C++ y qué es p en C#? (en uno de ellos p es un objeto y en el otro es una referencia a un objeto).**  
> Creo que en C++ es un objeto y en C# es una referencia a un objeto. 

🌱 **¿En qué parte de memoria se almacena p en C++ y en C#?**  
> Creo que en C++ está en el stack, porque el destructor se ejecuta po sí solo... y en C# quizás es heap?

🌿 **¿Qué observaste con el depurador acerca de p? Según lo que observaste ¿Qué es un objeto en C++?**  
>

___

# 📝 Actividad 07

En el stack: `0x000000B11418FB58`,  `0x0000000275B5FA68`, `0x000000FB1DAFF5A8`...    
En el heap: `0x000000B11418FB78`, `0x0000000C2036F848`, `0x000000886E11F508`, `0x0000000275B5FA88`...    
No entiendo por qué, cada vez que volvía a ejecutar el programa, la dirección de memoria de pHeap y pStack cambiaba?    


Nota: el formato para instanciar el objeto en el heap es MUY similar al de C#, por lo que creo que, efectivamente, en C# es también una referencia a un objeto.  

pStack: Objeto  
pHeap: Referencia a un objeto (al objeto Punto en el Heap)  

___

# 📝 Actividad integradora de aplicación
Errores:  
1. Creo que con `int* estadísticas` lo que está haciendo es crear un puntero hacia el array estadísticas. Luego utiliza asignación dinámica de memoria para asignar que `estadisticas = new int[3]`. Al ser memoria dinámica, el array queda almacenado en el Heap y luego **nunca lo borra**. Es totalmente innecesario... podría simplemente escribir `int estadisticas[3] = { 0,0,0 };` desde un inicio (se recomienda inicializar con valores default porque lo hace más predecible y evita errores al intentar acceder a un índice del array que no esté definidido).   
2. No tiene un destructor, por lo que los personajes creados no están siendo eliminados de la memoria.  
  
Corrección:  
```program.cpp
#include <iostream>
#include <string>

class Personaje {
public:
    std::string nombre;
    int estadisticas[3] = { 0,0,0 };

    Personaje(std::string n, int vida, int ataque, int defensa) {
        nombre = n;
        estadisticas[0] = vida;
        estadisticas[1] = ataque;
        estadisticas[2] = defensa;
        std::cout << "Constructor: nace " << nombre << std::endl;
    }

    ~Personaje()
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
