# Descripcion de la solución

A pesar de tener los videos correspondientes de simulación y de implementación, se considera apropiado generar una descripción general de la solución realizada
***
## Simulación en RobotStudio


***
## Implementación
Para la etapa de implementación, ya teniendo una simulación bastante acorde al montaje físico en el Labsir, es relativamente sencillo realizar los pasos necesarios para completar la implementación.

Lo primero es configurar el IRB140 a partir del proyecto que se realizó importándolo mediante una USB. Una vez importado, es posible tener las rutinas de movimiento y la herramienta llamada ToolAJA, donde su modelado corresponde con la herramienta física que se monta en el plato del brazo. Debido a esta semejanza de la herramienta entre la simulación y el montaje, no se consideró necesario calibrar el TCP, ya que las dimensiones corresponden adecuadamente a un movimiento de ingreso del marcador de 1cm, considerándose suficiente para su uso correcto, como ya se mencionó en la etapa de diseño de la herramienta.  

Ahora, a pesar de que el simulador ya tiene en cuenta las dimensiones del tablero inclinado, o el workobject, debido a la dificultad de posicionar el tablero tal cual como se hizo en RobotStudio, y el hecho de que la base del tablero no estaba sobre una superficie plana sino oblicua, los ejes coordenados del workobject en RobotStudio no van a corresponder con los de la implementación tanto en posición como en orientación. Debido a esto, se redefinió el sistema coordenado del workobject por el método de los 3 puntos, seleccionando en el mismo orden y los mismos vértices que se hizo en RobotStudio. Después de realizar este método, las nuevas coordenadas del origen workobject fueron (384.633, 165.518 225.431). Ya redefinido esto, se realiza la implementación inicial donde su video correspondiente se encuentra en la carpeta  **videos** como **video1**, y a continuación se muestran algunas de las imágenes del mismo proceso.


**Acercamiento a punto de seguridad:**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P11.png?raw=true)

**Inicio de primer trayectoria de dibujo:**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P12.png?raw=true)

**Resultado de primera trayectoria de dibujo:**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P13.png?raw=true)

**Finalizacion de trayectorias sobre tablero:**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P14.png?raw=true)

**Finalizacion con retorno a home:**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P15.png?raw=true)


Como se puede evidenciar en el video, o en su defecto en las imágenes expuestas, se realizaron correctamente los paths, y cabe aclarar que no hubo ninguna parada de emergencia o advertencia. Sin embargo, sí ocurrió un pequeño percance. Debido a la rapidez en el laboratorio en que se realizó la nueva referencia del workobject, no se generó completamente exacto con el vértice deseado del tablero, motivo por el cual cuando se generó el primer movimiento de ataque de las rutinas, a pesar de que no hubo daños en la herramienta o la base, se generó la suficiente fuerza para trasladar en Y un extremo del tablero. Es evidente el fallo en el extremo inferior izquierdo del dibujo de la primera **A**. Sin embargo, este movimiento del tablero fue de menos de un centímetro, y gracias a la capacidad de la herramienta de forzar la punta del marcador en dirección Z del TCP, se realizó adecuadamente la rutina y sus posteriores paths.

Ahora, para realizar una segunda trayectoria con diferentes coordenadas de trabajo del tablero, se generó un desplazamiento en Y positivo de 165mm, dejando las coordenadas del workobject en (384.633, 400.518 225.431). Así mismo, se movió físicamente el tablero esa distancia Y de aproximadamente 165mm sobre la superficie, estableciendo de manera concordante las referencias de este segundo workobject con el tablero físico. Definido este segundo caso, se realiza la implementación de manera efectiva y con resultados bastante similares a los obtenidos en el primer caso de la implementación.

**Inicio en Home (trayectoria 2):**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P21.png?raw=true)

**Inicio de primer trayectoria de dibujo (trayectoria 2):**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P22.png?raw=true)

**Resultado de primera trayectoria de dibujo (trayectoria 2):**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P23.png?raw=true)

**Finalizacion de trayectorias sobre tablero (trayectoria 2):**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P24.png?raw=true)

**Finalizacion con retorno a home (trayectoria 2):**

![Imagen inicial T1](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/P25.png?raw=true)

Con todo y lo anterior, incluso se puede decir que los resultados obtenidos en este segundo caso fueron mejores que en el primero, debido a que no hubo problemas de contacto o de movimientro entre el tablero y la herramienta. De este modo, se establece que es posible realizar un mismo conjunto de instrucciones con diferentes objetos de trabajo, ya sea redefiniendo su orientación, posición, o incluso ambos.

