# Bitácora de aprendizaje de la unidad 7

### 📝 Actividad 01   
🌱 **Incluye una captura de pantalla del ejemplo funcionando en tu máquina.**  
<img width="1846" height="1054" alt="image" src="https://github.com/user-attachments/assets/ef80b4ba-cf72-419d-b843-621f8dddfa16" />  

  
🌿 **Observa el proyecto, trata de entenderlo, pero ten presente que lo analizaremos más adelante.**  
> Viendo el proyecto, entiendo que solamente modificaste el archivo de triangle.cpp. El archivo que se llama glad.c parece que se generó automáticamente con el generador del proyecto. En la carpeta de dependencias externas veo MUUUUUUCHAS cosas, lo cuál me intimida un poquito. En triangle.cpp, veo que se incluyen 3 bibliotecas o referencias (creo que eso es lo que son?): `iostream`, `glad/glad.h` y `GLFW/glfw3.h`. En cuanto a la estructura del código, se parece a los proyectos de p5.js en el sentido de que primero organiza la ventana, sus dimensiones, inputs... pero de ahí en adelante, ubico 0.  

🌼 **¿Qué preguntas te surgen al ver el código?. Anota al menos tres preguntas que te gustaría investigar más adelante (no te preocupes que la idea de esta unidad es que las resuelvas).**  
> 1. Cuál es la diferencia entre vertexShaderSrc y fragmentShaderSrc?  
> 2. Qué es un VAO/VBO?  
> 3. Qué pasa si el frameBuffer no tiene el mismo tamaño que la ventana?  
> 4. Qué hace el V-Sync?  
  

___
### 📝 Actividad 02

🌻 **Necesito que hagas digestión de esta información y que la entiendas. Para ello te voy a pedir un resumen en tus propias palabras de lo que acabas de leer. En tu resumen debes tratar de conectar GLFW, opengl32.lib, GLAD, GLM y los drivers de la GPU. ¿Qué rol cumple cada uno? ¿Cómo se relacionan entre sí? Mira, trata de hacer esto de memoria y como si estuvieras contándole a un amigo que quiere aprender OpenGL. Cuando haces el proceso de memoria tu cerebro hace un esfuerzo adicional y eso te ayuda a aprender. Además, si no recuerdas algo quiere decir que no lo entendiste bien y eso es una buena señal para que vuelvas a leerlo.**
> 1. Crear un nuevo proyecto de C++ en visual studio, así vacío  
> 3. Buscarlo en el explorador de Windows  
> 4. crear una carpeta llamada external  
> 5. crear 3 carpetas para cada una de las dependencias a las bibliotecas (OpenGL, GLFW y GLAD)  
> 6. Se descarga glfw-3.4.bin.WIN64.zip del github de GLFW en la sección de releases y se descomprime. Esas carpetas van dentro de la que creamos para su cosito en external.  
> `PARÉNTESIS: GLFW me deja crear ventanas y manejar los inputs de teclado, mouse y esas cosas).`  
> 6. voy al sitio web de GLAD y genero el código fuente para OpenGL 4.6 y el perfil Core.
> 7. Descargo el archivo zip y guardo los directorios src e include en la carpeta que también cree en el cosito de external del proyecto. 
> `PARÉNTESIS: GLAD accede a las funciones de OpenGL mientras se ejecuta el programa.`  
> 8. se descarga el archivo glm-1.0.1-light.zip del repositorio de GLM en Github (versión 1.0.1)
> 9. Guardo completa la carpeta que se descomprime dentro del cosito de external
> 10. Abro el proyecto en VS y agrego las rutas de las dependencias a las propiedades del proyecto. (property -> C/C++ -> additional include directories)
> 11. Se agrega la dirección de las bibliotecas .lib. Solamente hay una en el proyecto. (property -> Linker -> general -> additional library directories)
> 12. En (property -> input -> additional dependencies), agregar esa biblipteca y una adicional: opengl32.lib
> 13. click derecho al proyecto en Visual Studio, Add/New item, agregar el archivo glad.c que se encuentra en la carpeta glad/src.
> 14. asegurarse de que el archivo glfw3.dll esté en el directorio principal del proyecto.
>  
>  En resumen, opengl viene con windows, GLAD me deja ejecutar esas funciones en tiempo real (porque no se pueden acceder de otra forma), GLFW me deja abrir pestañas y manejar inputs. Los .lib son dependencias necesarias con la info para las funciones, y .dll tiene el código como tal que se ejecuta. GLM es opcional y sirve para dibujar figuritas en 3d y hacer cálculos.


___
### 📝 Actividad 03

🌱 **RESUMEN:** yo quiero hacer algo, uso opengl para mandar la orden, GLAD hace de intermediario y le dice a la GPU lo que quiero, la GPU lo dibuja en el framebuffer, el framebuffer se pone en la ventana (creada por GLFW) después de haber sido dibujado por aparte.  
🌿 **EXPERIMENTO:** no entiendo qué hace `16) Intercambia buffers y muestra el contenido`, entonces voy a comentar la línea `glfwSwapBuffers(mainWindow);`y ver qué pasa. Tampoco entiendo qué hace el V-Sync, entonces después voy a comentar `glfwSwapInterval(1);`  

  > **Resultado 1:** lit sale todo negro en la pantalla.
  
  <img width="441" height="449" alt="image" src="https://github.com/user-attachments/assets/e2f36523-0229-43cc-ba02-1184709280ff" />  

  > **Resultado 2:** se pintó normal
  
  <img width="399" height="432" alt="image" src="https://github.com/user-attachments/assets/749e80c5-af0a-4e4b-a408-46e71cf404fd" />
  
  **Mi predict:** es como el draw en p5.js. Está cambiando la hojita dondel la GPU pintó cada x tiempo que le indica la línea de swap interval. Si no está la linea de cambiar el buffer, pues la aplicación nunca me manda la hojita invisible donde dibujó el triángulo. Por eso se ve negro.
___
🌼 **Experimentos con glDrawArrays:**
`GL_LINES:` solamente me dibujó una raya que une los dos vértices de abajo. Cambiando el tercer parámetro a 4 me dibujó una línea más desde el centro hasta el vértice de arriba.  
`GL_POINTS:` dibujó solo puntos en las posiciones de los vértices
`Tercer parámetro a 2:` no se dibujó nada
`Tercer parámetro a 4:` se dibujó normal
___
🌻 **Conceptos explicados con mis palabras:**
**¿Qué es el contexto OpenGL?**
> lo que utilizo para explicarle a la GPU lo que quiero dibujar. Ya viene con windows y tiene un montón de funciones y herramientas para hacer de todo, pero toca acceder a esas funciones con GLAD.  

**¿Cuál es el rol de la biblioteca GLFW y qué ventaja tiene usarla?**
> crea las ventanas donde se dibujan las cositas y maneja los inputs. Deja escribir código distinto para cada OS.

**¿Por qué crees que OpenGL necesita un contexto (recuerda la analogía del taller de arte)?**
> porque si no, no tiene de dónde sacar la info de las cosas que necesita para pintar.  

**¿En últimas qué será el framebuffer y a qué te recuerda de las dos primeras unidades del curso?**
> framebuffer sería el lugar donde se dibujan las figuras antes de mostrarse en la pantalla. De computacionales... no sé qué me recuerda. Pero de físicos interactivos, me recuerda al canvas que se actualizaba en Draw() de p5.js.  

**¿Qué relación entre en el viewport y el framebuffer?**
> Viewport es la ventanita con las dimensiones (como el marco), y framebuffer el dibujito como tal (como la hojita que va en el marco)  

**¿En todo la analizado hasta ahora qué rol juega los drivers de la GPU y la GPU misma?**
> La GPU es la que dibuja. Los drivers, no estoy segura.  

**¿Por qué crees que sea necesario activar el VSync? ¿Si no lo activas y la imagen es estática qué crees que pase, y si es dinámica?**
> Si es estática, yo creo que nada. Si es dinámica, me imagino que salen como blinks de negro en la pantalla mientras cambia de posición.  

**En esta unidad estamos usando OpenGL moderno, pero ¿Qué es OpenGL Legacy? ¿Qué diferencias hay entre ambos?**
> No sé, no lo recuerdo en la explicación D:

**¿Qué es el shader program? ¿Por qué es importante en OpenGL moderno?**
> todos los cositos que hicimos al inicio que definen cómo se procesan los vértices.  

**Trata de revisar el código setupTriangle(), intuitivamente ¿Qué crees que hace? ¿Qué crees que es el VAO y el VBO?**
> Creo que el VAO almacena los datos de los vértices, pero el VBO no estoy segura... asumo que tiene que ver con cómo se dibujan en el framebuffer.  

**En el ciclo principal (game loop) de OpenGL, notaste que en cada frame (cuadro) le decimos a openGL que use el shader program y el VAO. Si le indicas esto antes del game loop ¿Será necesario seguirlo haciendo en cada loop? Si no es necesario ¿En qué casos crees que esto puede ser útil?**
> No, creo que no sería necesario. Y creo que es porque podríamos tener múltiples shaders y objetos. Es más claro y flexible hacerlo en cada frame, aunque en este ejemplo simple no sea estrictamente necesario.

**Finalmente, recuerda lo que hace glfwSwapBuffers(mainWindow); ¿Por qué crees que es importante? ¿Qué pasaría si no lo llamas? ¿Cómo explicas lo que pasa si no lo llamas? (experimenta)**
> Porque el dibujito puede cambiar y animarse cada frame. SI no lo llamo, es como tener un video en pausa... hay más contenido para mostrar, y todo el video está ahí listo para verse, pero yo nunca estoy pasando del frame donde lo paré.


___
### 📝 Actividad 04

