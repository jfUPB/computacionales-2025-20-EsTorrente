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
