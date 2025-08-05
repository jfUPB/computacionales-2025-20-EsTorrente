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
  
**🌿Considera que los datos del arreglo están almacenados desde la dirección 16. Inicializa el arreglo en lenguaje ensamblador.**  
```program.asm

```
  
**🌼Simula paso a paso el programa en ensamblador. Recuerda la metodología: predice, ejecuta, observa y reflexiona.**  
>
  
**🌻Construye tu programa PASO A PASO mediante pruebas. Indica qué característica vas a implementar con cada prueba y cómo la probaste.**  
>
  
**🌱Muestra el programa final y cómo lo probaste.**  
>
  
