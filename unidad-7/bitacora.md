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

🌱 **Luego de estudiar las unidades 1 y 2 de este curso y ver el video, escribe con tus propias palabras ¿Cuál es la diferencia entre una CPU y una GPU?**  
> CPU ejecuta tareas en secuencia (paso por paso) pero es más especializada para cositas complejas. GPU deja que la CPU haga otros cálculos mientras, y se usa más para cositas gráficas como renderizar en blender porque puede hacer MUCHAS cosas de una.  

🌿 **Preguntas:**
**¿Cuáles son los tres pasos claves del pipeline de OpenGL? Explica en tus propias palabras cuál es el objetivo de cada paso.**
> `Vertex Shader:` Procesa cada vértice (posición, transformaciones)
> `Rasterización:` Convierte las figuras en píxeles
> `Fragment Shader:` Decide el color de cada píxel

**La gran novedad que introduce OpenGL moderno es el pipeline programable. ¿Qué significa esto? ¿Qué diferencia hay entre el pipeline fijo y el programable? ¿Qué ventajas le ves a esto? y si el pipeline es programable, ¿Qué tengo que programar?**
> Me imagino que la diferencia sería que el fijo es como una plantilla, y el programable te deja a ti tener full control sobre cada paso. Como en unreal, que te dan la opción de programar con nodos que ellos ya hicieron, o directamente hacerlo todo desde 0 con scripts de c++.  Me imagino que lo que tienes que programar es la forma en la que cada shader funciona, cuándo se llaman, cómo varía su comportamiento, los frames a los que el buffer se actualiza, esas cosas.  

**Si fueras a describir el proceso de rasterización ¿Qué dirías?**
> Agarrar los vértices que componen una figurita y calcular cuáles de los pixeles de la pantalla están dentro de esos vértices para poder dibujarlo.  

**¿Qué son los fragmentos? ¿Es lo mismo un fragmento que un pixel? ¿Por qué?**
> Sí, pero no. Los fragmentos son grupitos de pixeles que están en la misma figurita y tienen la misma textura/color. Dos pixeles pueden no ser del mismo fragmento, pero cada fragmento está compuesto por pixeles.   
  
**Explica qué problema resuelve el Z-buffer y ¿Qué es el depth test?**
> Define qué figuritas están más al frente y son visibles. Si hay varias figuritas muy cerquita en el axis z, empiezan como a buggearse una encima de otra. Le agrega datos más precisos a cada vértice para que pueda definir con más acertada su posición respecto a la cámara. Así dibuja solamente los colorcitos y texturas de lo que está más al frente.  

**¿Por qué se presenta el problema de la aliasing? ¿Qué es el anti-aliasing?**
> Porque pintan todos los pixelitos de un triángulo con full textura y opacidad del color, entonces todo se ve muy cuadriculado. El anti-aliasing suaviza esos bordes oscureciendo un poquito los pixeles de los bordes, y así, como los pixeles están junticos, se van como mezclando para el ojo y se ve mucho más suavecito.    

**¿Qué relación hay entre la iluminación y el fragment shader? Siempre es necesario tener en cuenta la iluminación en un fragment shader? o puedo hacer un fragment shader sin iluminación? Explica que implicaciones tiene esto.**
> El fragment shader CALCULA la iluminación y su efecto en los fragmentos dependiendo del material, pero no es obligatorio. Por ejemplo, en un modelo 3D tipo anime, tener sombras realistas calculadas hace que se vea HORRENDO porque las formitas no son naturales para una cara humana, y por ende, tampoco las sombras. Tener un material al que no lo afecta la luz en absoluto sino que tiene un color constante ayuda a imitar esa sensación de dibujito anime 2D.    

**¿Qué implica para la GPU que una aplicación tenga múltiples fuentes de iluminación?**  
>La GPU tiene que hacer más cálculos por cada fuente de luz adicional.  

🌼 **Escribe un resumen en tus propias palabras de lo que se necesita para dibujar un triángulo en OpenGL.**  
> 1. Crear ventana con GLFW  
> 2. Configurar VBO con datos de vértices    
> 3. Configurar VAO para decir cómo leer el VBO  
> 4. Compilar shaders (vertex + fragment)  
> 5. En cada frame: limpiar, usar shader, bind VAO, dibujar  
  
🌻 **Escribe un resumen en tus propias palabras de lo que necesitas para poder usar un shader en OpenGL.**  
> 1. Escribir código GLSL  
> 2. Compilar cada shader por separado  
> 3. Linkearlos en un programa  
> 4. Usar glUseProgram() para activarlos  


___
### 📝 Actividad 05
<img width="426" height="459" alt="image" src="https://github.com/user-attachments/assets/375a30e5-d273-46ea-b547-b38fc0f26da9" /> <img width="420" height="437" alt="image" src="https://github.com/user-attachments/assets/55fa6ad4-5eb7-40f0-98d9-90de729e26dd" /><img width="399" height="436" alt="image" src="https://github.com/user-attachments/assets/1c806cb5-0d64-4eea-9a96-ffdca6c095eb" /><img width="417" height="441" alt="image" src="https://github.com/user-attachments/assets/5d250132-abe1-43eb-aad3-598d9403d64e" />  

🌱 **Explica el proceso de normalización de las coordenadas del mouse y cómo se relaciona con el sistema de coordenadas de OpenGL.**
> Las coordenadas del mouse vienen en píxeles de la ventana (ej: 150, 200). Las normalizo dividiendo entre el ancho y alto de la ventana para convertirlas a un rango de 0 a 1. Esto me permite mapear fácilmente a otros sistemas de coordenadas.
  
🌿 **Explica el proceso de normalización a coordenadas de dispositivo (NDC) y cómo se relaciona con el sistema de coordenadas de OpenGL.**
> Primero, organizas X y Y para que sea un valor entre 0 y 1. OpenGL usa coordenadas de -1 a 1. Para convertir de mis coordenadas normalizadas (0-1) a NDC, dentro de los uniform:
> En el color, lo dejas igual... de 0 a 1 para X y Y. Pero para la ubicación del triángulo:  
> `X:` x * 2 - 1 = convierte `0 -> -1`, `0.5 -> 0`, `1 -> 1`  
> `Y:` 1 - y * 2 = convierte `0 -> 1`, `0.5 -> 0`, `1 -> -1` (invierte el eje Y porque en pantalla Y va hacia abajo, pero en OpenGL va hacia arriba)

___
## 📝 APPLY

🌱 **Cambios:**
1. Agregué un nuevo uniform time en el fragment shader  
2. Obtengo el tiempo usando glfwGetTime() dentro del loop principal  
3. Envío el tiempo al shader con glUniform1f(timeLocation, currentTime) en cada frame (timelocation indica el uniform, currentTime es el que tiene el valor del tiempo. Dentro del uniform estaba declarado que la variable del shader de fragmentos que modifico es el time :P)  

🌿 **Código:**
```cpp
#include <iostream>
#include <glad/glad.h>
#include <GLFW/glfw3.h>

// Callback: ajusta el viewport cuando cambie el tamaño de la ventana
void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
	glViewport(0, 0, width, height);
}

// Procesa entrada simple: cierra con ESC
void processInput(GLFWwindow* window) {
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}

// Tamaño de las ventanas
const unsigned int SCR_WIDTH = 400;
const unsigned int SCR_HEIGHT = 400;

// Fuentes de los shaders
const char* vertexShaderSrc = R"glsl(
	#version 460 core

	layout(location = 0) in vec3 aPos;
	uniform vec2 offset;

	void main() {
		vec3 newPos = aPos;
		newPos.x += offset.x;
		newPos.y += offset.y;
		gl_Position = vec4(newPos, 1.0);
	}
)glsl";

const char* fragmentShaderSrc = R"glsl(
	#version 460 core

	out vec4 FragColor;
	uniform vec4 ourColor;
	uniform float time;

	void main() {
		// usando seno para R y G, coseno para B :P
		float r = (sin(time) + 1.0) / 2.0;        // tira datos entre 0 y 1
		float g = (sin(time + 2.0) + 1.0) / 2.0;  // lo muevo más para que no sea lo mismo q el seno 1 zzz. Valores entre 0 y 1
		float b = (cos(time) + 1.0) / 2.0;        // lo mismo q el seno 1
		
		FragColor = vec4(r, g, b, 1.0);
	}
)glsl";

// IDs globales
unsigned int VAO, VBO;
unsigned int shaderProg;

// Compila y linkea un programa de shaders, retorna su ID
unsigned int buildShaderProgram() {
	int success;
	char log[512];

	unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
	glShaderSource(vs, 1, &vertexShaderSrc, nullptr);
	glCompileShader(vs);
	glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(vs, 512, nullptr, log);
		std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
	}

	unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
	glShaderSource(fs, 1, &fragmentShaderSrc, nullptr);
	glCompileShader(fs);
	glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(fs, 512, nullptr, log);
		std::cerr << "ERROR FRAGMENT SHADER:\n" << log << "\n";
	}

	unsigned int prog = glCreateProgram();
	glAttachShader(prog, vs);
	glAttachShader(prog, fs);
	glLinkProgram(prog);
	glGetProgramiv(prog, GL_LINK_STATUS, &success);
	if (!success) {
		glGetProgramInfoLog(prog, 512, nullptr, log);
		std::cerr << "ERROR LINKING PROGRAM:\n" << log << "\n";
	}

	glDeleteShader(vs);
	glDeleteShader(fs);
	return prog;
}

// Crea un VAO/VBO con los datos de un triángulo
void setupTriangle() {
	float vertices[] = {
		-0.5f, -0.5f, 0.0f,
		 0.5f, -0.5f, 0.0f,
		 0.0f,  0.5f, 0.0f
	};
	glGenVertexArrays(1, &VAO);
	glGenBuffers(1, &VBO);

	glBindVertexArray(VAO);
	glBindBuffer(GL_ARRAY_BUFFER, VBO);
	glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
	glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
	glEnableVertexAttribArray(0);
	glBindVertexArray(0);
}

int main()
{
	// 1) Inicializar GLFW
	if (!glfwInit()) {
		std::cerr << "Fallo al inicializar GLFW\n";
		return -1;
	}
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	// 2) Crear ventana
	GLFWwindow* mainWindow = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Triangulo pero más slay", nullptr, nullptr);
	if (!mainWindow) {
		std::cerr << "Error creando ventana1\n";
		glfwTerminate();
		return -1;
	}

	// 3) Lee el tamaño del framebuffer
	int bufferWidth, bufferHeight;
	glfwGetFramebufferSize(mainWindow, &bufferWidth, &bufferHeight);
	
	// 4) Callbacks 
	glfwSetFramebufferSizeCallback(mainWindow, framebuffer_size_callback);

	// 5) Cargar GLAD y recursos en contexto de window1
	glfwMakeContextCurrent(mainWindow);

	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
		std::cerr << "Fallo al cargar GLAD (contexto1)\n";
		return -1;
	}

	// 6) Habilita el V-Sync
	glfwSwapInterval(1);

	// 7) Compila y linkea shaders
	shaderProg = buildShaderProgram();

	// agregado uniform de time
	glUseProgram(shaderProg);
	int offsetLocation = glGetUniformLocation(shaderProg, "offset");
	int colorLocation = glGetUniformLocation(shaderProg, "ourColor");
	int timeLocation = glGetUniformLocation(shaderProg, "time");

	// 8) Genera el contenido a mostrar
	setupTriangle();

	// 9) Configura el viewport
	glViewport(0, 0, bufferWidth, bufferHeight);

	// 10) Loop principal
	while (!glfwWindowShouldClose(mainWindow))
	{
		// 11) Manejo de eventos
		glfwPollEvents();

		// 12) Procesa la entrada
		processInput(mainWindow);

		// 13) Configura el color de fondo y limpia el framebuffer
		glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
		glClear(GL_COLOR_BUFFER_BIT);
		
		// 14) Indica a OpenGL que use el shader program
		glUseProgram(shaderProg);

		// agarra tiempo actual con la función que mencionaste :P
		float currentTime = (float)glfwGetTime();
		glUniform1f(timeLocation, currentTime);

		// Dibuja el triángulo
		double xpos, ypos;
		glfwGetCursorPos(mainWindow, &xpos, &ypos);

		// Normalizo las coordenadas del mouse
		float x = (float)xpos / (float)SCR_WIDTH;
		x < 0 ? x = 0 : x;
		x > 1 ? x = 1 : x;

		float y = (float)ypos / (float)SCR_HEIGHT;
		y < 0 ? y = 0 : y;
		y > 1 ? y = 1 : y;

		// Envio el color y la posición del triángulo
		glUniform4f(colorLocation, x, y, 0.0f, 1.0f);
		glUniform2f(offsetLocation, x * 2 - 1, 1 - y * 2);

		// 15) Activa el VAO y dibuja el triángulo
		glBindVertexArray(VAO);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		// 16) Intercambia buffers y muestra el contenido
		glfwSwapBuffers(mainWindow);
	}

	// 17) Limpieza
	glfwMakeContextCurrent(mainWindow);
	glDeleteVertexArrays(1, &VAO);
	glDeleteBuffers(1, &VBO);
	glDeleteProgram(shaderProg);

	glfwDestroyWindow(mainWindow);
	glfwTerminate();
	return 0;
}
```
🌼 **Explica cómo usaste la función de tiempo (sin, cos, u otra) para lograr el efecto de cambio de color cíclico. ¿Qué rango de valores produce tu cálculo y cómo afecta eso al color final?**
> El seno lo usé para el r y g del rgb. El coseno para el b. Así solitos, tiran valores de -1 y 1... y eso no me sirve para colores, entonces toca mapearlo. Problema: que yo estoy acostumbrada a rgb de 255 como valor, entonces no entendía por qué tú no mapeaste tu color en el ejemplo de la actividad 1 a más de 0 y 1. Me fui a buscar, y es que al parecer opengl usa ese rango para rgb. Muy hater. Pero bueno, 0 problemas. Entonces modifiqué el seno y el coseno sumándole 1 y dividiéndolo entre 2. Así, si el dato es -1, = 0. Si es 0, = 0. Si es algo en medio, no importa. Si es 1, = 1.    
  
🌻**Incluye una captura de pantalla o UN ENLACE a un video mostrando el resultado del triángulo con color cambiante.**  
 > lo hice en base al de la actividad 5, entonces igual sigue el mouse... pero lo voy a dejar en un solo punto para la captura para que veas que sólo el tiempo es lo que lo cambia :>
  
<img width="420" height="444" alt="image" src="https://github.com/user-attachments/assets/6ec6522c-99c6-47c0-89c7-28a7ddbb5147" /> <img width="410" height="441" alt="image" src="https://github.com/user-attachments/assets/6a47ab32-72bc-4233-a0be-fb08b342db4b" /><img width="422" height="421" alt="image" src="https://github.com/user-attachments/assets/6eaf5c36-3bba-47d5-8a76-abcca3ae8041" /><img width="405" height="440" alt="image" src="https://github.com/user-attachments/assets/0f2b722f-fb05-4e78-be0f-85097e6c7b55" />

🌱 ¿Qué otros efectos visuales simples podrías lograr usando el tiempo como uniform? Piensa en la posición, el tamaño o la rotación (aunque no hemos visto rotaciones formalmente, ¡intuitivamente podrías intentarlo!). Anota al menos una idea.
> Que vaya pulsando también haciéndose más grande o más pequeño, que se vaya moviendo un poquito a la derecha e izquierda con suavizado para que se sienta como que está colgando del mouse, que vaya a la posición contraria del mouse (o sea, si el mouse está en x=1, el triángulo va a x=-1)...

___

# 📝 Autoevaluación

### 🌱 **Nota Propuesta: 5**

| Actividad | Evaluación | Justificación / Evidencias |
|-----------|------------|----------------------------|
| ⭐ 01 | Excelente | Demostré comprensión inicial del entorno OpenGL. Identifiqué correctamente la estructura del proyecto y las bibliotecas clave (`iostream`, `glad/glad.h`, `GLFW/glfw3.h`). Formulé preguntas fundamentales que , como siempre me pasa, tú mismo planteaste y explicaste después: diferencia entre shaders, propósito de VAO/VBO, relación framebuffer-ventana, y función del V-Sync. |
| ⭐ 02 | Excelente | Comprendí completamente el proceso de configuración de un proyecto OpenGL desde cero. Mi resumen detalló paso a paso la organización de dependencias (GLFW, GLAD, GLM) y demostró comprensión clara de los roles de cada componente: GLFW para ventanas/inputs, GLAD como intermediario de funciones OpenGL, y la diferencia entre archivos .lib y .dll. Internalicé la arquitectura de trabajo entre CPU, GPU y las bibliotecas de soporte. |
| ⭐ 03 | Excelente | Realicé experimentación activa y análisis crítico del pipeline gráfico. Mis pruebas con `glfwSwapBuffers()` demostraron comprensión práctica del double buffering. Experimenté exitosamente con `glDrawArrays` probando diferentes primitivas (GL_LINES, GL_POINTS) y parámetros. Mis explicaciones mostraron dominio de contexto OpenGL, framebuffer, viewport, y la relación CPU-GPU. |
| ⭐ 04 | Excelente | Me vi el video completo de 20 minutos. Identifiqué correctamente los tres pasos clave (Vertex Shader, Rasterización, Fragment Shader) y su propósito. Mi análisis del pipeline programable vs fijo incluyó analogías creativas (Unreal Engine nodes vs scripts) y comprendí las implicaciones prácticas. Resumí los conceptos avanzados vistos en el video como Z-buffer, anti-aliasing, y la relación iluminación-fragment shader, incluyendo ejemplos aplicados (estilo anime). Mis resúmenes fueron concisos y precisos. |
| ⭐ 05 | Excelente | Implementé exitosamente interactividad mediante uniforms, comprendiendo y aplicando el concepto de variables globales en shaders, normalización de coordenadas de mouse a diferentes sistemas (pantalla 0-1, NDC -1 a 1), y manejo correcto de la inversión del eje Y. El programa corrió correctamente. |
| ⭐ 06 (APPLY) | Excelente | Cumplí con el objetivo de modificar el color con el tiempo. Implementé un nuevo uniform `time`, usé funciones trigonométricas (sin/cos) para ciclos de color, y comprendí perfectamente el mapeo matemático de `-1 -> 1` a `0 -> 1` para valores RGB. Mi código completo funciona correctamente. Generé ideas adicionales creativas (pulsación, movimiento suave, posición invertida). |
  
