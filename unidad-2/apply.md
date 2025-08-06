# Unidad 2


## 🛠 Fase: Apply

### 📝 Actividad 06
```program.cpp
int arr[] = {1,2,3,4,5,6,7,8,9,10};
int sum = 0;

for (int j = 0; j < 10; j++) {
    sum = sum + arr[j];
}
```

**🌱Implementa el programa anterior en lenguaje ensamblador aplicando el concepto de punteros.**  
```program.asm
@i
M=0

(ARREGLO)
//subir contador
@i
M=M+1

D=M
A=D
M=D

//check arreglo
@10
D=D-A
@ARREGLO
D;JLT

@i
M=0
@SUMA
0;JMP

(SUMA)
@i
D=M
@sum
M=D+M

//CHECK
@9
D=D-A
@FIN
D;JGT

//SUBIR CONTADOR
@i
M=M+1
@SUMA
0;JMP

(FIN)
@FIN
0;JMP
```
> Aquí no había leído que debía empezar en la dirección 16, entonces lo hice desde 1 :(  
> También están un poquito raros los checks... y sé que me tocaría usar una variable que me sirva de puntero, pero si la creo usando @p y @i, van a ocupar la posición que necesito para el array. Me va a tocar simplemente usar directamente el número de la memoria RAM. Voy a usar:  
> - `RAM[0]` para @i  
> - `RAM[1]` para @suma  
> - `RAM[2]` para @p  
  
**🌿Considera que los datos del arreglo están almacenados desde la dirección 16. Inicializa el arreglo en lenguaje ensamblador.**  
```program.asm
//inicializar las variables
@16 // -> ahora sí lo empiezo en 16 :>
D=A
@2 //el puntero
M=D //p = 16 (me lleva al inicio del arreglo)


@0 // -> variable @i. No puedo usar @i pq ocupa el 16.
M=0
@1 // -> variable @sum
M=0


(LLENAR)
//check para ver si sigue en el loop
@0
D=M
@10
D=D-A
@FIN_LLENAR
D;JEQ //pq como empieza en 0, cuando llega a i = 10 ya es la onceava iteración


//guardar el número en la memoria
@0
D=M
D=D+1
@2
A=M // carga la posición RAM[16] en el primer ciclo
M=D // guarda ahí el numerito correspondiente a la iteración del ciclo (1 en el primer loop, pq le suma +1).


//pasar a la siguiente posición de memoria
@2 //vuelve a cargar la posición del puntero
M=M+1
@0
M=M+1 //i++
@LLENAR
0;JMP //salto incondicional a volver a empezar, pq ya había checkeado antes si salía o no del loop.

(FIN_LLENAR)
@16
D=A
@2 //carga el puntero
M=D //le asigna al puntero la posición donde inicia el array

@0
M=0 //reinicia el valor de i

(SUMAR)
//check
@0
D=M
@10
D=D-A
@FIN //revisa si ya pasó las 10 iteraciones
D;JEQ

//sumar
@2
A=M //carga en A el valor que esté en el puntero (16 en primera iteración)
D=M //guarda en D el valor que está en la posición 16 (1)
@1 //carga @suma
M=D+M //guarda en la memoria de suma el valor que estaba almacenado en la RAM[p] + lo que ya había en suma

//avanzar +1 en la dirección del array
@2
M=M+1

//i++
@0
M=M+1
@SUMAR
0;JMP

(FIN)
@FIN
0;JMP
```
  
**🌼Simula paso a paso el programa en ensamblador. Recuerda la metodología: predice, ejecuta, observa y reflexiona.**  
> Ahora sí, con las correcciones que hice en base a mi primera versión del programa, todo funcionó exactamente como esperaba. :>

  
**🌱Muestra el programa final y cómo lo probaste.**  
<img width="1258" height="892" alt="image" src="https://github.com/user-attachments/assets/59552852-8499-4023-8a3d-e6b7fa884095" />

  

