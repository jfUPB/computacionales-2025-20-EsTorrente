# Unidad 3

## 🔎 Fase: Set + Seek
### 📝 Actividad 01

🌱 **¿Para qué sirven los breakpoints?**  
> es un punto que asignamos manualmente para detener el código, evitando que se ejecute completamente y permitiéndonos revisarlo línea a línea. Facilita demasiado el encontrar el punto exacto donde algo no funciona como debería. Es como lo mismo que hacíamos en el simulador Hack.  
  
🌿 **¿Para qué se usa la ventana de depuración Autos?**  
> Como los registros en el simulador, nos permite revisar el valor actual asignado a cada variable y seguir la manera en la que éstos van cambiando línea a línea.  

___
### 📝 Actividad 02
🌱 **Predicción (antes de ejecutar):**
> a, b y c no son variables globales. Dentro de cada una de las funciones, se está usando un parámetro para modificar el valor. En el primer caso, como no se está modificando directamente una variable global, creo que simplemente crea como una copia de los valores y los modifica sólo dentro del método.  
> En el segundo caso... no sé si está buscando la dirección de la variable y modificándolo desde ahí? como habían explicado en clase que el símbolo & se utiliza para referenciar a la posición de la variable en la memoria. Y como no está usando * para modificar el valor en esa posición, entonces no estoy segura de si va a funcionar? creo que modificaría la posición de la variable, no el valor.
> En el tercer caso, al llamar el método en el main se le pasa como "&c", o sea que se le está mandando la ubicación de la memoria RAM. Luego, en el parámetro lo recibe como int*, por lo que asumo que ahí sí está agarrando el valor que está almacenado en ese lugar. Finalmente, como en la operación se utiliza *n, creo que el número sí se modifica directamente en la variable original.  

🌿 **Diferencias en comportamiento (después de ejecutar):**
> Mi predicción para el primer método era correcto... pero en el segundo sí logró modificar directamente el valor de la variable original, al igual que el tercero. En el tercer método fue necesario utilizar &c para indicar la posición de la variable y * para el valor, mientras que en el segundo sólo fue necesario utilizar &.  
  
🌼 **¿Por qué?**
> Porque, mirando bien el nombre del método, me doy cuenta de que en la segunda función el símbolo `&` es una REFERENCIA a la variable original, no directamente su ubicación, porque NO ES UN PUNTERO!!
> El tercer método SÍ LO ES, por lo que ahí el símbolo `&` sí está cumpliendo el rol de enviar la dirección de memoria de la variable.  
  
🌻 **MI PROGRAMA:**

```program.cpp
#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void swapPorValor(int a, int b) {

    cout << "Valor inicial a: " << a << endl;
    cout << "Valor inicial b: " << b << endl;

    int temp = a; //porque si le asigno a "a" el valor de "b", ya no lo puedo intercambiar
    a = b;
    b = temp;

    cout << "Dentro de swapPorValor, valor modificado a: " << a << endl;
    cout << "Dentro de swapPorValor, valor modificado b: " << b << endl;
}

// Función que modifica el parámetro pasado por referencia
void swapPorReferencia(int& a, int& b) {

    cout << "Dentro de swapPorReferencia, valor inicial a: " << a << endl;
    cout << "Dentro de swapPorReferencia, valor inicial b: " << b << endl;

    int temp = a;
    a = b;
    b = temp;

    cout << "Dentro de swapPorReferencia, valor modificado a: " << a << endl;
    cout << "Dentro de swapPorReferencia, valor modificado b: " << b << endl;
}

// Función que modifica el parámetro utilizando punteros
void swapPorPuntero(int* a, int* b) {
    cout << "Dentro de swapPorPuntero, valor inicial a: " << *a << endl;
    cout << "Dentro de swapPorPuntero, valor inicial b: " << *b << endl;

    int temp = *a;
    *a = *b;
    *b = temp;

    cout << "Dentro de swapPorPuntero, valor modificado a: " << *a << endl;
    cout << "Dentro de swapPorPuntero, valor modificado b: " << *b << endl;
}

int main() {
    int a = 1;
    int b = 2;

    cout << "===================================================\n";

    cout << "Valor inicial de a: " << a << endl;
    cout << "Valor inicial de b: " << b << endl;

    cout << "===================================================\n";

    cout << "\nLlamando a swapPorValor..." << endl;
    swapPorValor(a, b);
    cout << "===================================================\n";
    cout << "Despues de swapPorValor, valor de a: " << a << endl;
    cout << "Despues de swapPorValor, valor de b: " << b << endl;
    cout << "===================================================\n";

    cout << "\nLlamando a swapPorReferencia..." << endl;
    swapPorReferencia(a, b);
    cout << "===================================================\n";
    cout << "Despues de swapPorReferencia, valor de a: " << a << endl;
    cout << "Despues de swapPorReferencia, valor de b: " << b << endl;
    cout << "===================================================\n";

    cout << "\nLlamando a swapPorPuntero..." << endl;
    swapPorPuntero(&a, &b);
    cout << "===================================================\n";
    cout << "Despues de swapPorPuntero, valor de a: " << a << endl;
    cout << "Despues de swapPorPuntero, valor de b: " << b << endl;
    cout << "===================================================\n";

    return 0;
}
```
___
### 📝 Actividad 03

| Segmento de código | Variables globales y estáticas | Heap | Stack |
|--------------------|--------------------------------|------|-------|
| Instrucciones dentro de funcionConStatic(), crearArrayHeap(), suma() y main() | global_inicializada, global_no_inicializada, mensaje_ro, var_estatica | dirección de la memoria donde se almacena el array | int tam, int a, int b, int c, int tamArray, return arr, return c, return 0 |

___
### 📝 Actividad 04
🌱 **Experimento 1:**
> Se está itentando modificar la dirección de memoria del main. Lanza error porque se encuentra en el segmento de código, y ese es sólo de lectura. El programa se interrumpe en la línea 18.   
    
🌿 **Experimento 2:**
> Como el mensaje es sólo de lectura, al intentar reescribirlo saldrá un error. Las constantes en general no deberían cambiar durante la ejecución del programa.  
    
🌼 **Experimento 3:**
> Las variables globales sí se pueden modificar. La que fue inicializada comienza en el valor asignado y cambia a 69 luego de ser modificada,  mientras que la no inicializada es utomáticamente asignada el valor inicial de 0. Ese valor es modificado más tarde por 666. 
  
🌻 **Experimento 4:**
> Sale un mensaje de error diciendo que `var_estatica` no está definida, y el programa no se ejecuta. Es porque la variable estática solamente podrá ser utilizada dentro de la función donde se inicializó. Cuando una variable no es estática, se borran y crean cada que la función se ejecuta y finaliza. Cuando sí es estática, permanece almacenada en la memoria durante toda la ejecución del programa y se comparte entre todas las instancias de esa misma clase.  
  
🌱 **Experimento 5:**
> Ambas variables están siendo inicializadas dentro de la función, pero esa línea sólo está asignando el valor en la variable no estática. Como la variable estática sólo se crea e inicializa una vez en la primera ejecución del programa, toma el valor inicial de 100 e incrementa por 1 cada vez que esta se ejecuta. Por otro lado, la función no estática es creada, toma el valor de 100, suma +1 y luego es destruida en cada una de las iteraciones.  

🌿 **Experimento 6:**
> El programa lanza un error cuando se intenta escribir el valor en el ArrayHeap[0] porque esa parte de la memoria ya ha sido borrada. La línea que debe comentarse es `//delete[] arrayHeap;`, lo cuál permite que se ejecute correctamente y escriba el valor "10" al final. La memoria en el stack se borra automáticamente al salir de las funciones, mientras que en el stack toca hacer la asignación y eliminación manualmente. Si no se libera, puede llegar a ocupar cantidades grandes de la memoria y provocar que todo el sistema corra más lento.  
___
### 📝 Actividad integradora de investigación

🌱 **¿Cuál será la salida final en la consola de este programa?**  
> Creo que va a ser:  
> `Valor inicial de A: 20`  
> `Dentro de sumaPorValor, 'a' ahora es: 30`  
> `Valor final de val_A: 20`  
> `Valor inicial de B: 20`  
> `Dentro de sumaPorValor, 'b' ahora es: 30`  
> `Valor final de val_B: 30`  
> `Valor inicial de C: 20`  
> `Dentro de sumaPorValor, 'c' ahora es: 30`  
> `Valor final de val_C: 30`  
> --- Experimento con variables estáticas ---  
> `Llamada a ejecutarContador. Valor de contador_estatico: 1`   
> `Llamada a ejecutarContador. Valor de contador_estatico: 2`  
> `Llamada a ejecutarContador. Valor de contador_estatico: 3`  
> El contador global ni se usa ni se escribe.  
  
🌿 **Dibuja un mapa de memoria conceptual de este programa justo antes de que main finalice. Debes indicar en qué segmento de memoria (Stack, Heap, Datos Globales/Estáticos, Código) se encontraría cada una de las siguientes variables: contador_global, contador_estatico, val_A, val_B, val_C (dentro de main), el parámetro a de la función sumaPorValor, la función main misma.**  
  
| Código | Globales / estáticas | Heap | Stack |
|--------|----------------------|------|-------|
| main() | contador_global, contador_estatico | N/A | val_A, val_B, val_C |

El parámetro a de la función sumaPorValor (CREO QUE) ya no estaría almacenado en el stack, porque solamente aparece mientras se ejecuta la función...  
  
``︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶  ``
  
🌼 **Compara la salida real con tu predicción. Si hubo diferencias, explica por qué ocurrieron. Evidencia clave: capturas de pantalla antes y después de los puntos de interés (¿Cuáles son esos puntos? -> tu tarea analizarlo).**
> No hubo diferencias :>  
Después de inicializar las variables val_A, val_B, val_C (lo puse en esta otra ventana de locals porque en la normal al darle f5 -> f10 me estaba borrando el valor de A cuando salía C >:( ) :  
<img width="950" height="442" alt="image" src="https://github.com/user-attachments/assets/a3ceb164-4e9c-45c2-aff5-faf34ac7eb36" />
val_A se mantiene igual.
    
Después de llamar sumaPorReferencia:  
<img width="920" height="581" alt="image" src="https://github.com/user-attachments/assets/8d6b9c48-2a24-4e34-9344-6ad4bb721389" />  
val_B cambia a 30.  
  
Cuando estoy llamando sumaPorPuntero:  
<img width="928" height="425" alt="image" src="https://github.com/user-attachments/assets/31e79e50-8af4-4ff0-8a44-6245f0bc8275" />  
toma &val_c como una variable, en Autos me dice que su valor es `0x0000001e9f56f8a4 {20}` y que su tipo es	`int *`. Asumo que está diciendo que ese número súper largo es la dirección de la memoria, el 20 el valor almacenado en ella, y es un int* porque es un puntero.  
  
Después de llamar sumaPorPuntero:  
<img width="931" height="372" alt="image" src="https://github.com/user-attachments/assets/b901bceb-9bd1-4426-903e-325f78490fe2" />  
Ahora en el valor de &val_c sale `0x0000001e9f56f8a4 {30}`, y en el valor de val_C sale 30.  

Después de llamar ejecutarContador() 3 veces:  
<img width="930" height="323" alt="image" src="https://github.com/user-attachments/assets/972cc71d-7add-4c2f-b16d-5edeba25888e" />  
No aparece ningún cambio  ni variable en Autos. No sé por qué no se muestra el cambio del valor del contador ni la variable en general... puede ser porque no está en esa sección de la memoria que Autos trackea?  
  
``︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶  ``
  
🌻 **Describe qué demuestran estas capturas sobre la diferencia entre los diferentes tipos de paso por parámetros analizados.**
|Primera captura | Por valor | Por referencia | Por puntero |
|----------------|-----------|----------------|-------------|
| Muestra los valores iniciales de las 3 variables | La captura demuestra que el valor de val_A luego de ejecutarse sigue siendo exactamente igual | la captura demuestra que el valor está cambiando luego de ejecutarse, por lo que sé que se altera directamente la original | mostró cómo se llamaba la dirección en la memoria de la variable, cómo modificaba el valor almacenado en dicha región, y que demostró que el cambio es directo a val_C | 

🌱 **Explica con tus propias palabras el comportamiento de contador_estatico. ¿Por qué “recuerda” su valor entre llamadas a la función ejecutarContador? ¿En qué se diferencia de una variable local normal?**  
> Las variables locales normalitas se inicializan y destruyen cada vez que se llama la función correspondiente. No se comparten entre instancias de objetos. Por otro lado, las variables estáticas mantienen ese valor almacenado y compartido entre todas las instancias de los objetos de esa clase, y se inicializan solamente en la primera ejecución. No se destruye cuando se sale de la función que le corresponde.  
