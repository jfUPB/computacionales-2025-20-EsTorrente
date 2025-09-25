# Bitácora de aprendizaje de la unidad 6

### 📝 Actividad 1
🌱 **¿Cómo puedes interactuar con la aplicación? Menciona específicamente las teclas y qué efecto parecen tener sobre las partículas.**
<a name="Capturas"></a>
> `Tecla a`: atrae a las partículas hacia la posición del mouse. Como si fuera un campo gravitacional.
  
<img width="867" height="651" alt="image" src="https://github.com/user-attachments/assets/9328fca2-8563-4bb0-8f58-2db61eaf45aa" />  
  
> `Tecla r`: repele a las partículas, haciendo que "huyan" de la posición del mouse. Como si fuera un imán con otros del mismo polo, ejerciendo una fuerza en dirección opuesta.
  
<img width="1013" height="756" alt="image" src="https://github.com/user-attachments/assets/ba9f7562-cce2-4dac-bf95-3343101789af" />
  
> `Tecla s`: detiene a las partículas. Hace que se congelen en la posición actual y no reaccionen al mouse hasta actualizar de nuevo el efecto.
  
<img width="1014" height="757" alt="image" src="https://github.com/user-attachments/assets/10adc41a-350b-4c61-b62f-bc5a6d484e16" />
  
> `Tecla n`: el estado default. Las partículas flotan en direcciones random y con velocidades distintas. No tiene interacción con el mouse.
  
<img width="1012" height="760" alt="image" src="https://github.com/user-attachments/assets/15dbf74d-2e4f-4bef-81e9-2f4ed8e86664" />
  
🌿 **¿Observas los diferentes tipos de “partículas”? ¿Se comportan todas igual inicialmente?**
> Como tal, la clase partícula no tiene subclases. Lo que hace que sean varios tipos es que en la creación de las partículas se le asignan distintos atributos. En el OffApp.cpp sí se inician las partículas como conjunto con unos atributos base, pero luego, desde el setup, se le está diciendo al programa que cree 100 partículas star, 5 shooting stars, 10 planets con el método `createParticle`. En ese método se modifican los atributos default de acuerdo al string con el que se envió la partícula al método. Para star, solamente cambian su tamaño y su color. Para shooting star, cambian su tamaño, su color y se le asigna una mayor velocidad (se multiplica la default x 3). Para planets, sólo se modifica su color y su tamaño. En ese sentido, sí podría decirse que la clase Particle se inicia con el mismo comportamiento, pero es inmediátamente modificado en setup.  

🌼 **Toma algunas capturas de pantalla de la aplicación en diferentes momentos (estado inicial, después de presionar ‘a’, ‘r’, ‘s’, ‘n’) y añádelas a tu bitácora.**  
> Puse las capturas [aquí, en la primera pregunta](#Capturas). 

🌻 **¿Qué crees que está pasando “detrás de cámaras” cuando presionas las teclas? Formula una hipótesis inicial sobre cómo la aplicación cambia el comportamiento de las partículas.**
> En el estado de stop, la velocidad es 0 (no hay movimiento). En el estado normal, se le asigna una velocidad random que se le suma a su posición. Para repelerla y atraerla, me imagino que la posición de la partícula está siendo sumada o restada por la posición del mouse... al mismo tiempo, creo que la velocidad se estaría multiplicando por el valor de una fuerza que actúa sobre ella.

___

### 📝 Actividad 2


