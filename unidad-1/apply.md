# Unidad 1

## 🛠 Fase: Apply
___
## 📝 **Actividad 03**  

Escribe un programa que compare el valor almacenado en la dirección de memoria 5 con el valor 10. Si el valor es menor que 10, guarda el valor 1 en la dirección 7. Si el valor es mayor o igual a 10, guarda el valor 0 en la dirección 7.  

```programa1.asm
(COMPARACION)
@5
D=M
@10
D=D-A
@MAYOR
D;JGE
@MENOR
0;JMP

(MENOR)
@1
D=A
@7
M=D
@FINAL
0;JMP

(MAYOR)
@0
D=A
@7
M=D

(FINAL)
@FINAL
0;JMP
```
︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶

> **🌱Análisis:** en mi primera versión del programa, no agregué el loop de final. Cuando lo ejecuté, caí en cuenta de que (obviamente) estaba ejecutando el bloque (MAYOR) inmediatamente después de terminar (MENOR). También aprendí en este ejercicio que no tenía que introducir el valor que iba a estar en la memoria RAM[5] desde la memoria ROM, sino que podía modificarlo directamente en la consolita del simulador.

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
___

## 📝 **Actividad 04**  

Crea un programa que use un ciclo para sumar los números del 1 al 5 y guarde el resultado en la dirección de memoria 12.

```program2.asm
(INICIO)
@12
M=0
@i
M=1

(CICLO)
@i
D=M
@5
D=D-A
@FINAL
D;JGT

(SUMA)
@i
D=M
@12
M=D+M
@i
M=M+1
@CICLO
0;JMP

(FINAL)
@FINAL
0;JMP
```

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶

> **🌱Análisis:** ya es un poquito más fácil trabajar con las variables. Los loops no son tan complicados ahora, pero sí me toca un poco cambiar el chip de mi cerebro que estaba acostumbrado a hacerlo como en C#. No es un cambio muy drástico, pero me puede enredar en detallitos chiquitos. A mi cerebro aún le cuesta ver @12 no solo como el valor de registro A, sino también al mismo tiempo la posición en la memoria RAM... y M como el valor en esa posición, no sólo la ubicación. También descubrí que tenía un error de sintaxis! cuando intentaba cargar el programa, la memoria ROM me salía totalmente en 0. Me puse a eliminar línea por línea hasta darme cuenta que el problema estaba en "M=D+M", que originalmente había escrito como "M=M+D". Parece que la D siempre debe ir primero en esa operación. Luego de corregir eso, cargó con normalidad.

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
