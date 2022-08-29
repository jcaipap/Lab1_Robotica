# Laboratorio 1 de Robótica
### Presentado por:
#### Andrés Holguín Restrepo 
#### Julián Andrés Caipa Prieto
### Presentado a: 
#### Ing. Ricardo Emiro Ramírez H.
#### Ing. Jhoan Sebastian Rodriguez R.

## Introducción 
El laboratorio #1 de la asignatura brinda un acercamiento inicial diseño y uso de herramientas, mediante la programación de rutinas asociadas a seguimiento de caminos modelados, tanto en simulación como en práctica con el uso de los robots disponibles. 

Se tienen los siguientes resultados de aprendizaje esperados:
- Realizar calibración de herramientas en el robot real, así como en Robot Studio.
- Identificar los tipos de movimientos en el espacio de la herramienta útiles para trabajos de manipulación.
- Ampliar el manejo de funciones proporcionadas por Robot Studio.

El trabajo se desarrollará sobre 3 ejes temáticos, el diseño de la herramienta, el proceso de calibración simulación/práctica y la generación de la rutina del robot. 

La idea principal del laboratorio es diseñar e implementar una herramienta que permita fijar un marcador borrable al flanche del robot, y generar la rutina para que dicha herramienta dibuje las iniciales de los integrantes (presente caso "AJA") sobre una superficie ubicada en el espacio de trabajo que cuenta con una cierta inclinación. 

## Diseño de la herramienta
Para el diseño y fabricación de la herramienta se planteó el uso de tubos PVC, unidos mediante una conexión de tubería tipo "T". Dichos tubos cuentan con un espesor de *Introducir espesor*. La idea del uso de la conexión es ubicar la herramienta de forma perpendicular al flanche del robot, lo que permite una manipulación más sencilla. 
*Foto tubos*

Además el marcador instalado se le colocan unos anillos de retención de goma tipo empaque, esto para que se sostenga al interior del tubo. 
*Foto marcador con empaques*

Debido a que el robot ejerce fuerzas considerables sobre el marcador, lo ideal sería tener un sistema de retroceso que impida que la punta del marcador se fracture o se meta dentro del mismo. Para esto se realiza un corte en la tapa del marcador y se ubican unos cauchos que facilitan el retroceso pero impiden que siga de largo.
*Foto cauchos*

La herramienta busca sostenerse al flanche mediante un tubo conectado al extremo libre de la "T", y a una pieza directamente al flanche, impresa en tecnología 3D, que tiene el siguiente diseño:
*Diseño conexión*

Finalmente la herramienta diseñada resulta como:
*Herramienta final*

Es de gran importancia contar con el modelo CAD de la herramienta, además que será de gran utilidad para procesos de calibración y diseño de trayectorías en RobotStudio. El modelo de la herramienta utilizando el software AutoDesk Inventor se presenta a continuación:
*Imagen modelo*

