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
## Orden de subcarpetas
En este repositorio se encuentran las siguientes subcarpetas con sus correspondientes contenidos:
- Diseño de la herramienta:  Explicación de metodología de diseño para la herramienta implementada.
- Código en RAPID: Código implementado tanto en simulación como en implementación del laboratorio.
- Videos: Videos generados en simulación como en implementación.
- Descripción de la solución: Explicación detallada del proceso de solución en RobotStudio para llegar a una simulación adecuada, y luego el proceso de implementación para realizar la implementación.

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







