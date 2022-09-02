# Laboratorio 1 de Robótica
## Universiad Nacional de Colombia
## 2022-2
***
### Autores
- Andrés Holguín Restrepo 
- Julián Andrés Caipa Prieto
### Profesores encargados
- Ing. Ricardo Emiro Ramírez H.
- Ing. Jhoan Sebastian Rodriguez R.
***
## Introducción 
El laboratorio #1 de la asignatura brinda un acercamiento inicial diseño y uso de herramientas, mediante la programación de rutinas asociadas a seguimiento de caminos modelados, tanto en simulación como en práctica con el uso de los robots disponibles. 

Se tienen los siguientes resultados de aprendizaje esperados:
- Realizar calibración de herramientas en el robot real, así como en Robot Studio.
- Identificar los tipos de movimientos en el espacio de la herramienta útiles para trabajos de manipulación.
- Ampliar el manejo de funciones proporcionadas por Robot Studio.

El trabajo se desarrollará sobre 3 ejes temáticos, el diseño de la herramienta, el proceso de calibración simulación/práctica y la generación de la rutina del robot. 

La idea principal del laboratorio es diseñar e implementar una herramienta que permita fijar un marcador borrable al flanche del robot, y generar la rutina para que dicha herramienta dibuje las iniciales de los integrantes "AJA" (A: Andrés; JA: Julián Andrés)  sobre una superficie ubicada en el espacio de trabajo que cuenta con una cierta inclinación. 
***
## Explicación de subcarpetas
En este repositorio se encuentran las siguientes subcarpetas con sus correspondientes contenidos:
- Diseño de la herramienta:  Imágenes relacionadas al diseño de la herramienta.
- Código en RAPID: Código implementado tanto en simulación como en implementación del laboratorio.
- Videos: Videos generados en simulación como en implementación con sus respectivas imágenes.

Mientras que en esta carpeta se tiene el informe realizado de la práctica.

***
## Diseño de la herramienta
Para el diseño de la herramienta, se plantea utilizar un marcador borrable "Expo". Para esto, la herramienta debe cumplir ciertos criterios para poder tener un mejor funcionamiento del IRB140 en la escritura de las iniciales de los nombres.

Lo primero, es que el marcador no debe estar en dirección normal al plato, ya que esto puede generar singularidades. De este modo, se establece que el marcador debe estar en dirección paralela a la superficie del plato. Además, para reducir posibles daños en el marcador y en la herramienta, se necesita tener una articulación prismática entre la herramienta diseñada y el marcador, con el fin de que al ejercer demasiada presión sobre el marcador, este pueda desplizarse sobre la herramienta en vez de dañar su punta y dejar de funcionar. Esto implica separar el diseño de la herramienta en dos:
- Articulación prismática entre el marcador y su soporte.
- Base de acople entre el soporte y el plato del IRB140.


### Soporte del marcador
Con base en lo mencionado anteriormente, se realizó un diseño de bajo costo el cual cumple con las especificaciones dadas. Lo primero fue utilizar una conexión en T de pvc de 3/4'', donde el orificio lateral se utiliza para el acople al plato y los otros dos orificios son utilizados para el marcador. Con esto, se colocan 6 empaques separados por pares en el marcador, los cuales permiten generar limites y estabilidad del movimiento prismático del marcador con respecto al agujero de la conexión T. A partir de esta configuración, se tiene un posible deslizamiento del marcador de casi 2cm, lo cual se considera suficiente como margen de seguridad ante la presión generada. Así mismo como los empaques generan estabilidad y límites en el movimiento, se utilizan cauchos en el extremo opuesto a la punta del marcador, donde se ubica la tapa del mismo,esto con el fin de que siempre se ejerza una presión suficiente para que la punta del marcador esté lo más extendida posible sin dañarla. por último, para facilitar la conexión entre la T y el acople soporte-plato, se utiliza un segmento de tubo de PVC de 3/4'' de 33mm de largo conectado al orificio lateral.

Toda esta explicación se muestra en las siguientes imagenes:

Marcador con sus empaques:

![Marcador y empaques](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/marcador.jpg?raw=true)

Conexión T con segmento de PVC lateral:

![Conexión T con segmento de PVC lateral](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/conT.jpg?raw=true)

Conjunto del soporte del marcardor:

![Conjunto del soporte del marcardor](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/conjSop.jpg?raw=true)

### Acople soporte-plato

Ya teniendo el soporte del marcador, se diseña el acople entre dicho soporte y el plato del IRB140. Para empezar, cabe describir ambas conexiones.  

Por un lado, la conexión al soporte debe realizarse mediante una conexión hembra-macho, donde se tiene un diámetro interno del tubo de PVC de 21.4mm medido con un pie de rey. Por el otro lado, el plato cuenta con la siguiente disposición de agujeros roscados:

![Dimensiones del plato del IRB140](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/plato.png?raw=true)

#### Modelado 3D

Con todo y lo anterior, se define la siguiente pieza para este acople:

![Modelo 3D soporte-plato](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/acople3D.png)

![Dimensiones del acople soporte-plato](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/base.png?raw=true)

Como se puede evidenciar, se cumplen las condiciones para el acople por tornillos M6 al plato, y una diferencia entre diámetros e 0.4mm entre la conexión macho-hembra, lo cual se contempló en caso de posibles imperfecciones en la impresión 3D.

#### Impresión 3D

A partir de este modelado 3D, se utiliza el software Repetier Host y una impresora 3D para generar la pieza. Cabe resaltar que, al ser una impresora propia, la calidad no es tan alta como lo hubiera sido mandar a imprimir. Se imprime en PLA con capas de 0.3mm de espesor y densidad de pieza del 20%. Los resultados de la impresión se muestran a continuación:

![Modelo 3D en Repetier-Host](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/3DRH.png?raw=true)

![Acople impreso](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/3DI.jpg?raw=true)


### Resultados finales de la herramienta

Con todo y lo anterior, se cuenta tanto con el soporte del marcador capaz de adaptar la punta del marcador a la superficie, y la base impresa en 3D para anclar la herramienta al plato del IRB140.

![Conjunto Separado Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/HfinalSeparada.jpg?raw=true)


Por último, se realiza el ajuste adecuado para que entre a presión la base de la herramienta con su conexión en T al enrollar la conexión macho con cinta de teflon. El resultado final se ve a continuación:
![Conjunto Unido Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/HfinalUnida.jpg?raw=true)

# Herramienta utilizada en RobotStudio
Ahora, para poder realizar una simulación adecuada en RobotStudio, es necesario tener el modelo de la herramienta lo más preisa posible, para esto, se generó en Inventor una pieza donde se tuviera tanto el marcador, soporte y acople, con el fin de definir el conjunto como herramienta de trabajo y definir adecuadamente el TCP. A continuación se muestra este modelo.


![Conjunto Unido Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/HerrRS.png?raw=true)




***
## Simulación en RobotStudio
Es necesario realizar la simulación en RobotStudio y desarrollar el código RAPID que permitirá crear las trayectorías que el robot deba seguir para el trazado de las letras sobre la superficie. 
Para ello se realiza el procedimiento estándar de inicio, se crea una nueva estación y se ubica el brazo a trabajar, en este caso el IRB140, disponible en la biblioteca de ABB. Posteriormente se genera un controlador asociado y se verifica el estado de este, comenzando a trabajar hasta que esté activo y disponible para su uso. _Poner imagen estación_


Posteriormente es necesario configurar la herramienta a trabajar y su respectivo TCP, para ello es conveniente desactivar la visibilidad del robot y para poder observar de mejor manera la herramienta a configurar.

El primer paso es importar la geometría de la herramienta, previamente diseñada y exportada como archivo .sat para facilidad. La geometría de la herramienta aparecerá en el centro de la estación, orientada como se modelo en el software de diseño (Autodesk Inventor en el presente informe). Ahora, se debe transformar la geometría importada en la herramienta requerida, para ello se sigue un procedimiento relativamente sencillo siempre y cuando se tenga la información pertinente, lo cual se explica a continuación. Primero se va a la pestaña de Modelado>Mecanismo>Crear Herramienta. Se abre un módulo como el siguiente: *Foto módulo*

En el módulo se asigna un nombre a la herramienta, se selecciona componente "Usar existente" y se selecciona la geometría importada. En los demás parámetros a modificar, se ingresan los valores adecuados de masa, inercia y centro de gravedad. Respecto a estos valores, suele utilizarse para herramientas más robustas o macizas, debido a que el robot debe compensar los efectos inerciales de esta, sin embargo, en el presente caso, la masa de la herramienta es muy baja, por lo cual no es de alta importancia a la hora de los calculos de las trayectorías. Se modifica la masa ingresando los 100 gramos que tiene la misma.
Posteriormente, se requiere ubicar el TCP de la herramienta. Para ello existen dos posibilidades, la primera es seleccionarlo en el espacio de trabajo de RobotStudio utilziando los comandos de selección y ubicando el punto de interés dentro del diseño. La segunda y más recomendable es obtener las coordenadas y orientación del punto de ubicación dicho TCP en la geometría utilizando el software en donde se diseño. Y se presiona finalizar y se tiene la herramienta creada con su respectivo TCP. Hablar del cambio de orientación

Por último, para anclar la herramienta la robot, se arrastra en el árbol de procesos hasta el robot y se acepta el cuadro de diálogo que indica sobre la actulización de la herramienta. Al activar la visibilidad del robot debería poder verse la herramienta en el plato del robot. *Insertar imagen herramienta puesta*


El siguiente paso a desarrollar es el objeto de trabajo. Para definir el Workobject se realiza de forma análoga a la herramienta, se importa una geometría sobre la cual se vaya a trabajar, en este caso es el diseño de objeto generado previamente, que contiene las letras en relieve para facilitar el diseño de trayectorías, y se ubica en la estación aproximadamente en la posición real que va ocupar sobre el área de trabajo. Posteriormente, se accede a Posición inicial>Otros>Crear objeto de trabajo; y en la ventana que se abre sobre el árbol de procesos, se selecciona la opción Sistema de coordenadas de usuario>Sistema de coordenadas por puntos, y se despliega el menú, sobre el cual se selecciona la opción "Tres puntos" y se dispone a seleccionarlos en la geometría del objeto de trabajo, esto para definir el sistema coordenado sobre el cual se va a trabajar. La selección de los tres puntos es recomendable sobre las esquinas del objeto, comenenzando en una superior y rotando en sentido antihorario. El objeto entonces adquiere su marco de referencia con el eje z posicionado normalmente a la superficie de este. 

Ya contando con la herramienta y el objeto de trabajo, se procede a definir las trayectorias para generar el código que se implementará en el robot. Para esto, primero es recomendable y adicionalmente requisito del informe, contar con una operación que genere el acercamiento desde Home a la pieza de trabajo para facilitar el posicionamiento del robot y sus artículaciones, y otra que lleve el robot a Home después del proceso. Otro par de consideraciones a tener en cuenta son:
- La posición asignada como Home suele escogerse, en la vida real el robot tiene todas sus artículaciones en 0 grados a excepción de la quinta, que se posiciona a 30 grados. Para el presente caso la posición de Home se seleccionó como 0 grados en todas las articulaciones. 
- Por ahora se van a utilizar dos tipos de "Target" o objetivos de posicionamiento a los cuales llegará el robot, y dos tipos de "Move" o movimientos que hace el robot para llegar a dicho Target.
- El primer movimiento se trata de uno de tipo lineal, y en este el robot pasa entre targets, los cuales se denominan "Punto", el cual representa una ubicación en el espacio a la cual llegará la herramienta, y dicho punto tiene su propio sistema de referencia coordenado, con lo cual el robot se orienta para posicionar el TCP en el sistema del punto y quedar en la posición y orientación definida por el target. 
- El segundo movimiento se trata de uno de tipo articular, en el cual el robot pasa de un estado de artículaciones a otro, llegando a unos targets denominados "Posición de ejes", en los cuales se coloca información sobre los grados a los cuales se van a posicionar las artículaciones del robot cuando se llegue a dicho target. 
- zona y velocidad xd







***
## Implementación
Para la etapa de implementación, ya teniendo una simulación bastante acorde al montaje físico en el Labsir, es relativamente sencillo realizar los pasos necesarios para completar la implementación.

Lo primero es configurar el IRB140 a partir del proyecto que se realizó importándolo mediante una USB. Una vez importado, es posible tener las rutinas de movimiento y la herramienta llamada ToolAJA, donde su modelado corresponde con la herramienta física que se monta en el plato del brazo. El montaje fue bastante básico, a partir del corercto diseño del acople de la herramienta y el plato, solo fue necesario utilizar dos tornillos M6x25 separados a 180 grados en el soporte, lo cual era suficiente para garantizar el montaje de la herramienta. De este modo, debido a esta semejanza de la herramienta entre la simulación y el montaje, no se consideró necesario calibrar el TCP, ya que las dimensiones corresponden adecuadamente a un movimiento de ingreso del marcador de 1cm, considerándose suficiente para su uso correcto, como ya se mencionó en la etapa de diseño de la herramienta.  

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




