# Unidad 2

## 🔎 Fase: Set + Seek

### 📝Actividad 01  

```programa.asm
@SCREEN
M=1
```
1. Va a la dirección de memoria de SCREEN
2. Le da el valor de 1
3. El primer número de derecha a izquierda se convierte en un 1, pintando el pixel de la esquina de arriba a la derecha
<img width="1159" height="184" alt="image" src="https://github.com/user-attachments/assets/862436d3-285a-43be-ad1b-1ba319dc0a52" />
<img width="472" height="62" alt="image" src="https://github.com/user-attachments/assets/6fc229c1-ff97-4d41-9db0-58df51a4a575" />
  
**🌱Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**
> Como aquí sí podría utilizar una variable con nombres claros, y lo que estoy haciendo es asignarle un valor a esa memoria:  
> screen = 1;  
> -> Con posición de memoria 16384 (no sé cómo asignarlo)  
___

### 📝Actividad 02  

```programa.asm
@SCREEN
M=-1
```
1. Va a la dirección de memoria de SCREEN
2. Le da el valor de -1
3. Todos los espacios de memoria en binario se convierten en 1, pintando los 16 pixeles asignados a es posición.
<img width="1366" height="190" alt="image" src="https://github.com/user-attachments/assets/e89fd724-328d-42d9-a525-b7f6e4f57ec8" />
  
**🌱Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**
> Como aquí sí podría utilizar una variable con nombres claros, y lo que estoy haciendo es asignarle un valor a esa memoria:  
> screen = -1;  
> -> Forzando posición de memoria 16384
>  
> **OTRA FORMA:**  
> 0xFFFF

___

### 📝Actividad 03  

```programa2.asm
@SCREEN
M=-1
@CONTADOR
M=0

(LEER)
@KBD
D=M
@100
D=D-A
@DERECHA
D;JEQ

@KBD
D=M
@105
D=D-A
@IZQUIERDA
D;JEQ

@LEER
0;JMP

(DERECHA)
//borrar dirección actual
@CONTADOR
D=M
@SCREEN
A=D+A
M=0


//mover
@CONTADOR
M=M+1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP

(IZQUIERDA)
//borrar dirección actual
@CONTADOR
D=M
@SCREEN
A=D+A
M=0

//mover
@CONTADOR
M=M-1
D=M
@SCREEN
A=D+A
M=-1

@LEER
0;JMP
```
1. Crea la línea negra asignando el valor de -1 a RAM[SCREEN].
2. Crea una variable con nombre CONTADOR y le asigna un valor inicial de 0
3. Lee el input del teclado, almacena ese valor en D. Le asigna a A el valor de 100 (el valor correspondiente a la tecla D) y lo resta al valor asignado en el registro D (la tecla que estaba presionada)
4. Si la resta = 0, eso significa que la tecla presionada corresponde a D, y hace un salto a (DERECHA). Si no, el programa se sigue ejecutando.
5. Vuelve a leer KBD, a guardar el valor de la tecla presionada, a restarle 105 (el valor correspondiente a la tecla i), y si = 0, salta a (IZQUIERDA). De lo contrario, el programa se sigue ejecutando y hace un salto incondicional a (JUMP)
6. En tanto (DERECHA) como (IZQUIERDA), lo primero que hace es borrar la línea de la dirección actual. Para esto, carga en A el valor actual del contador (a cuántos espacios de memoria más adelante del valor de @SCREEN se encuentra), asigan en D el valor del contador, carga el valor de SCREEN en A, y almacena en A el resultado de D+A (la posición actual de la línea).
7. Pone el valor de la memoria correspondiente en 0 para borrar la línea.
8. Vuelve a llamar al contador y le suma o le resta 1 (dependiendo de si quiere ir a la posición a la derecha o a la izquierda respectivamente).
9. Asigna a D el valor del contador
10. Vuelve a cargar screen, y suma el valor del contador para saber en cuál dirección de memoria dibujar la nueva raya. En esa posición asigna el valor de M=-1 para pintar el pixel de negro.
11. Al finalizar el movimiento, realiza un salto incondicional a (LEER) para volver a analizar el input del teclado. 
  
**🌱Traduce este programa a lenguaje C++ para que relaciones cómo los conceptos de alto nivel se traducen a bajo nivel.**  
Creo que se vería (sin asignar tipo de variables ni nada) algo así:
```program.cpp
screen = -1;
contador = 0;

while(true) {
    tecla = leerTecla();
    
    if(tecla == 100) { 
        (screen + contador) = 0;
        contador++;
        (screen + contador) = -1;
    }
    else if(tecla == 105) { 
        (screen + contador) = 0;
        contador--;
        (screen + contador) = -1;
    }
}
```
> En C# conozco Console.ReadLine(), pero no sé realmente cómo leer el teclado en C++...  
> Por eso sólo dejaré implícito que se está leyendo el teclado de alguna manera.
  
**🌱Como realmente se vería:.**  
```program.cpp

```
___ 

### 📝Actividad 05  
Convierte estos programas a ensamblador y realiza la simulación paso a paso. Recuerda la metodología: predice, ejecuta, observa y reflexiona.  
```program.cpp
int a = 10;
int* p;
p = &a;
*p = 20;
```
En ensamblador:
```program.asm
@10 //carga el 10
D=A //le asigna 10 a D

@a //crea variable a
M=D // a=10

@a //llama la posición de a
D=A //guarda la posición de la variable a en D
@p //crea variable p
M=D //p= la posición de a

@20 //carga número 20
D=A //lo asigna a D
@p //llama la posición de variable p
A=M //guarda en el registro a lo que estaba almacenado en p (que era la posición de memoria de la variable a)
M=D //reecribe en la memoria de a el valor 20
```
Segundo programa:
```program.cpp
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
```
En ensamblador:
```program.asm
@10
D=A

@a
M=D

@5
D=A

@b
M=D

@a
D=A
@p
M=D

//no he terminado esta parte final
@p
A=M
@b
M=D

```
___
### 🐟 NOTAS PARA MIGUEL VALENCIA QUE ESTABA SIENDO MUY JUICIOSO Y PRESENTANDO UNA PRUEBA: 🐟  
`C++:`  
PUNTERO: es una variable que guarda direcciones.  
`int i;` -> i es una variable donde se guarda un valor (un entero)  
  
> `int* ptr;` -> declara un puntero usando *  
> `ptr = nombre de la variable`  
> `* = guarda una dirección`  
> `int = el tipo de objetos de los que guarda la dirección.`  
  
> `int i = 5;`  
> `int* ptr = i;` -> NO FUNCIONA!!! no puedes guardar el valor de i en ptr, sólo la posición. Eso es lo que estarías haciendo ahí.

Lo que haría el puntero es APUNTAR al contenido de la variable en la memoria. Para esto se agrega:
> `int* ptr = &i;`, donde & es la definición de la variable. El & lo usamos para llamar la dirección de la variable. Ahí sí estarías guardando su posición.
  
Pero para guardar en una variable el valor de la variable a la que estás apuntando en ese momento en otra variable:  
> `int j = *ptr;`

Y para reescribir la variable a la que estás aputando:
> `*ptr = 25;`

🐡 En otras palabras:
> `&i` = para apuntar a la posición de una variable (apuntarle).  
> `*ptr` = para guardar o reescribir el valor que está almacenada en la variable a la que apuntas.
