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
D;JGT

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
🌼**Lo que hace:** 
1. Carga el valor que se encuentra en la memoria RAM[5] y lo almacena en D.
2. Carga el número 10 en el registro A.
3. En D, almacena el número que resulte de restarle A (10) a D (RAM[5])
4. Si el resultado es mayor que 0, eso significa que es mayor... así que salta a (MAYOR). Si es menor, el programa se sigue ejecutando y pasa a la sección de (MENOR).
5. En ambos casos, la sección (MAYOR) y (MENOR) cargan en el registro A el número asignado por el enunciado, lo almacenan en el registro D, luego cargan el valor de la memoria RAM[7] y le asignan en esa posición el valor de D. La diferencia es que, sin un salto al final de (MENOR), el programa ejecutaría de corrido (MAYOR). Por eso agregué un salto incondicional a una sección de (FINAL), donde no hay más operaciones y el PC se queda en un loop para evitar que siga ejecutando instrucciones que podrían dar problemas. (Leí que estaba recomendado hacer eso, no sé si sea verdad)

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶

> **🌱Análisis:** en mi primera versión del programa, no agregué el loop de final. Cuando lo ejecuté, caí en cuenta de que (obviamente) estaba ejecutando el bloque (MAYOR) inmediatamente después de terminar (MENOR). También aprendí en este ejercicio que no tenía que introducir el valor que iba a estar en la memoria RAM[5] desde la memoria ROM, sino que podía modificarlo directamente en la consolita del simulador. Además, no había ninguna indicación sobre qué hacer si el valor es IGUAL a 10, por lo que simplemente sigue corriendo el programa como si fuera un número menor.

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
🌻**Lo que hace:** 
1. En la sección de (INICIO) cargo la posición 12 (donde se almacena la suma) y la borro con M=0 para reiniciarlo (por si lo ejecuté antes)
2. Luego, como mostraba la documentación que se creaba un loop, creo una variable @i (que se asigna en RAM[16], según nos contaste) y le doy el valor de 1.
3. En la sección del ciclo, lo primero que hago es llamar la ubicación de i, que me dice en qué iteración vamos. Le asigno el valor que está en RAM[16] a D.
4. Cargo el número 5 en el registro A para utilizarlo en la siguiente operación.
5. En D almaceno D (el número de iteración actual) - A (5). Si el número es mayor que 0, es porque la i ya alcanzó un valor de 6 y el programa no debe continuar. Hace un salto incondicional a (FINAL). Si es igual o menor que 0, entonces i=5 o i<5, y el programa sigue a la sección de (SUMA).
6. En suma, vuelve a cargar el valor que hay almacenado en @i (RAM[16], el número actual de iteraciones) y se lo asigna a D.
7. Luego carla la posición de memoria 12, y en ella suma el valor de D (el número de iteraciones) + lo que ya se ha sumado y almacenado en RAM[12].
8. Vuelve a cargar la posición de i, y en la memoria (RAM[16]) toma el valor actual de iteración y le suma 1.
9. Salto incondicional a (CICLO) donde vuelve a revisar si ya llegó hasta i=6.
10. Se sigue repitiendo hasta saltar a (FINAL)

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶

> **🌱Análisis:** ya es un poquito más fácil trabajar con las variables. Los loops no son tan complicados ahora, pero sí me toca un poco cambiar el chip de mi cerebro que estaba acostumbrado a hacerlo como en C#. No es un cambio muy drástico, pero me puede enredar en detallitos chiquitos. A mi cerebro aún le cuesta ver @12 no solo como el valor de registro A, sino también al mismo tiempo la posición en la memoria RAM... y M como el valor en esa posición, no sólo la ubicación. También descubrí que tenía un error de sintaxis! cuando intentaba cargar el programa, la memoria ROM me salía totalmente en 0. Me puse a eliminar línea por línea hasta darme cuenta que el problema estaba en "M=D+M", que originalmente había escrito como "M=M+D". Parece que la D siempre debe ir primero en esa operación. Luego de corregir eso, cargó con normalidad.

︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶୨୧︶︶⊹︶︶⊹︶︶୨୧︶︶⊹︶⊹︶︶︶⊹︶︶
