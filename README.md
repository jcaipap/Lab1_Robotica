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

Mientras que en esta carpeta principal se tiene el informe realizado de la práctica.

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
Es necesario realizar la simulación en RobotStudio y desarrollar el código RAPID que permitirá crear las trayectorias que el robot deba seguir para el trazado de las letras sobre la superficie. 
Para ello se realiza el procedimiento estándar de inicio, se crea una nueva estación y se ubica el brazo a trabajar, en este caso el IRB140, disponible en la biblioteca de ABB. Posteriormente se genera un controlador asociado y se verifica el estado de este, comenzando a trabajar hasta que esté activo y disponible para su uso. 

![Estación](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S1.png?raw=true)


Posteriormente es necesario configurar la herramienta a trabajar y su respectivo TCP, para ello es conveniente desactivar la visibilidad del robot y para poder observar de mejor manera la herramienta a configurar.

El primer paso es importar la geometría de la herramienta, previamente diseñada y exportada como archivo .sat para facilidad. La geometría de la herramienta aparecerá en el centro de la estación, orientada como se modelo en el software de diseño (Autodesk Inventor en el presente informe). Ahora, se debe transformar la geometría importada en la herramienta requerida, para ello se sigue un procedimiento relativamente sencillo siempre y cuando se tenga la información pertinente, lo cual se explica a continuación. Primero se va a la pestaña de Modelado>Mecanismo>Crear Herramienta. Se abre un módulo como el siguiente:

![Crear herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S2.png?raw=true)

En el módulo se asigna un nombre a la herramienta, se selecciona componente "Usar existente" y se selecciona la geometría importada. En los demás parámetros a modificar, se ingresan los valores adecuados de masa, inercia y centro de gravedad. Respecto a estos valores, suele utilizarse para herramientas más robustas o macizas, debido a que el robot debe compensar los efectos inerciales de esta, sin embargo, en el presente caso, la masa de la herramienta es muy baja, por lo cual no es de alta importancia a la hora de los cálculos de las trayectorias. Se modifica la masa ingresando los aproximadamente 100 gramos que tiene la misma.
Posteriormente, se requiere ubicar el TCP de la herramienta. Para ello existen dos posibilidades, la primera es seleccionarlo en el espacio de trabajo de RobotStudio utilizando los comandos de selección y ubicando el punto de interés dentro del diseño. La segunda y más recomendable es obtener las coordenadas y orientación del punto de ubicación dicho TCP en la geometría utilizando el software en donde se diseño, en este caso esas coordenadas fueron (71.4, 0, 67.85). Luego se presiona finalizar y se tiene la herramienta creada con su respectivo TCP. Un detalle clave en la definición del TCP de la herramienta que será de alta utilidad en el momento de definir las trayectorias es que se ubico el eje z con una inclinación relativa, es decir, el eje z no es completamente perpendicular al eje normal de la punta del marcador, esto se realizó con el fin de que el ángulo de ataque en los movimientos disminuya las posibilidades de colisión entre el robot y la pieza. La inclinación se ajustó para que coincida con el corte diagonal de la forma de la punta de la herramienta. Puntualmente, este procedimiento se realizó mediante un giro en el eje Y de -20 grados, teniendo en cuenta que originalmente ya se había hecho un giro positivo de 90 grados sobre este mismo eje con el fin de cumplir el requerimiento del eje z.
*foto tcp*

Por último, para anclar la herramienta al robot, se arrastra en el árbol de procesos hasta el robot y se acepta el cuadro de diálogo que indica sobre la actualización de la herramienta. Al activar la visibilidad del robot debería poder verse la herramienta en el plato del robot. 

![Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S4.png?raw=true)


El siguiente paso a desarrollar es el objeto de trabajo. Para definir el Workobject se realiza de forma análoga a la herramienta, se importa una geometría sobre la cual se vaya a trabajar, en este caso es el diseño de objeto generado previamente, este se compone de una rampa generada al unir dos tableros cuadrados de 28.7cm de arista. A partir de esta definición, se genera su modelado y se realiza la inscripción de las iniciales de los integrandes del grupo **AJA**. A continuación se muestra una imagen de este objeto.

![Workobject](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/AJA.png?raw=true)


Una vez se importa este objeto, se ubica aproximadamente en la posición real que va ocupar sobre el área de trabajo, puntualmente, con origen en (500,200,0). 

Posteriormente, se accede a Posición inicial>Otros>Crear objeto de trabajo; y en la ventana que se abre sobre el árbol de procesos, se selecciona la opción Sistema de coordenadas de usuario>Sistema de coordenadas por puntos, y se despliega el menú, sobre el cual se selecciona la opción "Tres puntos" y se dispone a seleccionarlos en la geometría del objeto de trabajo, esto para definir el sistema coordenado sobre el cual se va a trabajar. La selección de los tres puntos es recomendable sobre las esquinas del objeto, comenzando en una superior y rotando en sentido antihorario. El objeto entonces adquiere su marco de referencia con el eje z posicionado normalmente a la superficie de este. 

Ya contando con la herramienta y el objeto de trabajo, se procede a definir las trayectorias para generar el código que se implementará en el robot. Para esto, primero es recomendable y adicionalmente requisito del informe, contar con una operación que genere el acercamiento desde Home a la pieza de trabajo para facilitar el posicionamiento del robot y sus articulaciones, y otra que lleve el robot a Home después del proceso. Otro par de consideraciones a tener en cuenta son:
- La posición asignada como Home suele escogerse, en la vida real el robot tiene todas sus articulaciones en 0 grados a excepción de la quinta, que se posiciona a 30 grados. Para el presente caso la posición de Home se seleccionó como 0 grados en todas las articulaciones. 
- Por ahora se van a utilizar dos tipos de "Target" o objetivos de posicionamiento a los cuales llegará el robot, y dos tipos de "Move" o movimientos que hace el robot para llegar a dicho Target.
- El primer movimiento se trata de uno de tipo lineal, y en este el robot pasa entre targets, los cuales se denominan "Punto", el cual representa una ubicación en el espacio a la cual llegará la herramienta, y dicho punto tiene su propio sistema de referencia coordenado, con lo cual el robot se orienta para posicionar el TCP en el sistema del punto y quedar en la posición y orientación definida por el target. 
- El segundo movimiento se trata de uno de tipo articular, en el cual el robot pasa de un estado de articulaciones a otro, llegando a unos targets denominados "Posición de ejes", en los cuales se coloca información sobre los grados a los cuales se van a posicionar las articulaciones del robot cuando se llegue a dicho target. 
- Hay dos parámetros que se deben tener en cuenta, que son de alta importancia a la hora de la implementación en la vida real del código desarrollado, que son la velocidad y la zona tolerable de errores. La primera se ajusta a un valor de 50, para evitar movimientos bruscos del robot y tener la posibilidad de visualizar con más detalle las trayectorias. En cuanto a la segunda, el máximo valor posible que se solicita es de z10, por lo cual se deja en este valor, para evitar comprometer los movimientos por exigencia de “finura” en el seguimiento de la trayectoria de trazado.
-	Dichos parámetros se pueden modificar de dos maneras, la primera es en la esquina inferior de la interfaz del programa, ubicando una región en la cual se encuentran dichos parámetros. Al cambiarlos allí, se afecta cualquier trayectoria que se cree después de cambiarlos, van a tener los valores puestos ahí. 

![Interfaz](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S5.png?raw=true)

- La segunda forma de cambiarlos es hacerlo en cada movimiento de una trayectoria específica. Para ello se selecciona el/los movimientos(s) a cambiar en el árbol de procesos, lo cual se explicará en breve, y se da clic derecho>Modificar una instrucción, y se cambia el parámetro que se desee. 
-	Finalmente, existen tres formas de crear trayectorias, por ahora se hará uso de dos de ellas, la primera es una “Trayectoria vacía”, en la cual se agregan a mano los targets a los cuales se desea recorrer durante esta, y el programa automáticamente asigna el tipo de movimiento a realizar con ellos. La otra es el uso de “Trayectoria automática”, en esta se realiza una selección a partir de geometrías ya establecidas en el espacio de trabajo, y se forma una cadena de targets de forma automática y la respectiva conexión entre ellos. En la trayectoria automática se pueden modificar ciertos parámetros que cambian la forma en la que el robot sigue la cadena de targets, que son los Offset de herramienta en la entrada y salida del movimiento, el tipo de aproximación que depende de la geometría de la trayectoria (en este caso se usa lineal), la distancia mínima que tendrán los targets generados, la tolerancia de desviación con respecto a la herramienta de la trayectoria, el máximo radio para circunferencias, y por último distancias de aproximación y partida, que son parámetros que permiten darle al robot una distancia perpendicular a la trayectoria antes y después de recorrerla.  En trayectoria automática es posible generar una cadena de targets que recorra todo un conjunto de aristas siempre y cuando estas conformen un camino cerrado, para ello se pulsa la tecla “Shift” y se selecciona cualquier arista perteneciente al camino cerrado.
Conociendo ya los conceptos claves para la definición de trayectorias, se procede a la definición de estas. Se van a definir dos trayectorias vacías para hacer el acercamiento y el retorno a Home, y cinco trayectorias automáticas para los movimientos de las letras, dos por cada letra “A” para el exterior y el triángulo del interior, y una para la letra “J”.  Es destacable que el proceso de generación de trayectorias, así como el proceso de generación de código RAPID y simulación suelen presentar múltiples errores comunes, los cuales se discutirán posteriormente y se dará posibles soluciones para ellos, teniendo en cuenta que las soluciones de mayor rango cuando no se llega a eliminar el error son reiniciar el controlador (Controlador>Reiniciar), crear un nuevo controlador, cerrar el programa y volver a abrirlo, o generar una estación completamente nueva y comenzar el proceso desde cero. El último se llevo a cabo 4 veces con propósitos de aprendizaje en el presente laboratorio. Otra consideración a destacar y que será de utilidad más adelante es que los targets de tipo punto, al tratarse de ubicaciones en el espacio, el robot puede tomar múltiples configuraciones de articulaciones para alcanzar dicho punto, lo cual será definitivo a la hora de trabajar en las trayectorias, ya que pasar de un target a otro que involucre cambiar las articulaciones pasando por una singularidad o por giros que el robot no puede dar, sea por colisión con el mismo o porque la articulación no puede hacer dicho giro porque se sale de sus límites. La configuración de articulaciones posibles de cada target se puede modificar manualmente para cada uno de los targets de tipo punto creados, haciendo en el target Clic derecho>Configuraciones, y seleccionando la más adecuada según lo deseado; o se puede hacer con todos los targets de una trayectoria haciendo uso de la función “Configuración automática” de la cual se hablará más adelante cuando se hable de la creación de trayectorias para las letras.

![Articulaciones](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S6.png?raw=true)

Para las primeras fue necesario crear 3 targets, los cuales se harán utilizando el tipo de target posición de ejes, para el Home se posicionaron todas las articulaciones en 0. Para las otras dos se utilizaron configuraciones cercanas a lo que define la trayectoria, es decir, perpendicular a una distancia seleccionada de aproximación, en este caso, 100mm para todas las trayectorias. Así se formularon dos targets, el primero con configuración 0,20,-20,40,-20,-20 respectivamente para las seis articulaciones, y el segundo con configuración 0,50,-40,70,-50,-50 respectivamente. Ahora se va a Posición inicial>Ruta>Trayectoria vacía, y se generan las dos trayectorias y se arrastran los tres targets a ellas y se posicionan de la manera adecuada según lo requerido. 

Para las trayectorias de las letras, se hará uso de trayectoria automática. Se crean las cinco trayectorias generando cadenas, en ellas solo se cambia la distancia de acercamiento y partida, que se ubican en 100mm. Inicialmente el programa genera las trayectorias y los respectivos puntos, pero al analizar el árbol de procesos y abrir cada una de las trayectorias, es muy posible que los movimientos muestren señales de advertencia (amarillo) o de error (rojo) sobre la flecha que los describe (de ahora en adelante A/E), ambos están asociados a configuraciones no posibles de las articulaciones del robot, sea porque pasando de un punto a otro se podría generar un error (de forma general las advertencias), o porque el robot entra en una singularidad (de forma general las rojas). Para corregir esto existen varias posibilidades, que deberían seguirse en un orden lógico para permitir hacer más consistente el movimiento. Inicialmente es ideal que, ya que cada punto tiene su propio sistema, que todos los puntos tengan la misma orientación, esto permitirá que el robot no deba hacer movimientos innecesarios respecto a los ejes para pasar de un target a otro en la cadena, sino que simplemente haga el movimiento de seguimiento de la cadena, incluso, sería una buena práctica hacer coincidir la orientación de todos los puntos de las cinco trayectorias, lo cual no se realiza en este caso, debido a errores generados, pero si se ajusta la orientación de forma equivalente para cada trayectoria. Para realizar esto lo ideal es seleccionar un target que este orientado de forma tal que no genere errores, es decir, ver cual movimiento no tiene A/E, y buscar el target asociado. Luego, se da Clic derecho>Copiar posición y orientación>En relación con objeto superior, y se seleccionan los demás targets de la trayectoria y se da Clic derecho>Aplicar posición y orientación>Orientación, y con esto se reorientan los targets. Si después de esto existen movimientos que persisten con A/E, entonces se busca el target asociado y se rota con respecto al eje z levemente hasta una posición hasta donde no ocurra esto (una buena práctica es rotar entre 5 a 10 grados), haciendo uso de Clic derecho>Modificar posición>Girar, y seleccionar el eje de interés. Luego, repetir el procedimiento de reorientación de los targets en conflicto, pero ahora con la orientación del recién corregido. Otra posibilidad y además buena práctica para evitar errores posteriores en la simulación de la trayectoria, es decir, que incluso sin errores es recomendable aplicar, es el uso “Configuración automática”, ya que al probar la trayectoria (Clic derecho>Moverse a lo largo de la trayectoria), es posible que se generen errores porque el robot no pueda alcanzar algún target desde la posición que se encuentra, o no pueda pasar de un target a otro. Configuración automática se ejecuta en la trayectoria (Clic derecho>Configuración automática>Todas las instrucciones de movimiento) y optimiza las configuraciones de articulaciones basándose en el target inmediatamente anterior en la cadena, así se evita tener que seleccionar una configuración para cada target, y adicionalmente se disminuye la posibilidad de caer en A/E porque el robot ejecuta los menores movimientos articulares posibles. 

![Configuración automática](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S7.png?raw=true)

Si aún después de todo esto, la trayectoria sigue presentando errores, la posible solución es ejecutar movimiento por movimiento y ver en cual se genera el error (dicho error se presentará sobre el panel de salida). Los más comunes son Error de posición del robot y Error de configuración del robot, aunque existen otros que se corrigen de forma análoga, siempre que dependan de la configuración articular del robot. El movimiento que presente error se puede corregir girando el target. Si finalmente se siguen presentando errores, se puede hacer uso de las soluciones habladas previamente como soluciones de mayor rango. 

El último procedimiento y más importante ya que generará el código a implementar en el robot en la vida real es la generación del código RAPID. Lo primero siempre es verificar que se tenga seleccionada la tarea, la herramienta y el objeto de trabajo adecuados, para ello se va a Posición inicial>Parámetros, y se estudia cada uno de ellos. De estar esto correctamente seleccionado, se pasa a Posición inicial>Controlador>Sincronizar y se escoge la opción que dice Sincronizar con RAPID, lo cual despliega un menú en el cual se debe seleccionar todo para que lo tenga presente la generación de código, y se da finalizar. 

![RAPID](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S8.png?raw=true)

Ya con esto generado, se va a Controlador y en el árbol de procesos RAPID>T_ROB1, y ahí se tienen dos códigos, el primero CalibData que almacena la información de la herramienta y el objeto de trabajo, y el otro Module1 (por defecto), que almacena todos los targets e instrucciones de las trayectorias creadas como objetos (de programación) y funciones respectivamente. Entre dichas funciones denotadas como PROC, existe una conocida como Main(), esta será la función principal que ejecute tanto la simulación como el robot, y es donde se realizará el llamado de las demás funciones, por lo cual se debe escribir sobre este el llamado a las funciones, en el orden que se desean ejecutar, escribiendo la misma seguido de “;” para cerrar la línea. 

![Main](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S9.png?raw=true)

Con todo y lo anterior, se procede a correr el código RAPID, para ello se va la pestaña RAPID>Probar y depurar. Lo ideal sería primero dar en Verificar programa para analizar posibles errores de escrituras de código. Luego dar Inicio, e idealmente se debería ejecutar todo el programa y trayectorias sin problema alguno. Realmente es probable que la ejecución presente errores, pero existen múltiples formas de corregirlos, debido a que generalmente se deben a posiciones del robot, esto descubierto gracias a darse cuenta de que en ocasiones el programa corría situando el robot en cierto punto, pero no desde Home, debido a que debía pasar por singularidades, y por ello la importancia de las rutinas intermedias de acercamiento a pieza y retorno a Home. La simulación en RAPID afecta también el módulo de Simulación, por tanto, es ideal que al tener cualquier fallo y querer correr de nuevo el código, se vaya allá y se detenga la simulación y se reestablezca (en este módulo también se pueden detener simulaciones de trayectorias como las hechas anteriormente para verificar). En ocasiones el programa se queda atascado en alguna simulación que le generó error, por lo cual en la pestaña de RAPID es recomendado detener todos los procesos, y reiniciar el controlador. Para poder analizar a detalle qué línea de código genera error, se puede usar la opción RAPID>Probar y depurar>Paso a paso por instrucciones, hasta encontrar la instrucción en conflicto y retornar a Posición inicial para corregirla desde las trayectorias y targets allá, haciendo rotaciones o analizando el movimiento para ver porqué ocurre el error. Después de dichas correcciones, es ideal cargar de nuevo el programa RAPID sincronizando y reiniciando el controlador.

Finalmente, al comprobar que todo el programa se corre sin presentar errores, ya está listo para exportarse y ser implementado. Para ello se va a Controlador, y en el árbol de procesos RAPID>T_ROB1, se da Clic Derecho>Guardar programa cómo, lo cual generará una carpeta en el computador que almacena el código que se utiliza en el Robot, específicamente en el FlexPendant. 

![Carpeta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Videos/imagenes/S10.png?raw=true)

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




