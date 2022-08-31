# Diseño de la herramienta
Para el diseño de la herramienta, se plantea utilizar un marcador borrable "Expo". Para esto, la herramienta debe cumplir ciertos criterios para poder tener un mejor funcionamiento del IRB140 en la escritura de las iniciales de los nombres.

Lo primero, es que el marcador no debe estar en dirección normal al plato, ya que esto puede generar singularidades. De este modo, se establece que el marcador debe estar en dirección paralela a la superficie del plato. Además, para reducir posibles daños en el marcador y en la herramienta, se necesita tener una articulación prismática entre la herramienta diseñada y el marcador, con el fin de que al ejercer demasiada presión sobre el marcador, este pueda desplizarse sobre la herramienta en vez de dañar su punta y dejar de funcionar. Esto implica separar el diseño de la herramienta en dos:
- Articulación prismática entre el marcador y su soporte.
- Base de acople entre el soporte y el plato del IRB140.

***
## Soporte del marcador
Con base en lo mencionado anteriormente, se realizó un diseño de bajo costo el cual cumple con las especificaciones dadas. Lo primero fue utilizar una conexión en T de pvc de 3/4'', donde el orificio lateral se utiliza para el acople al plato y los otros dos orificios son utilizados para el marcador. Con esto, se colocan 6 empaques separados por pares en el marcador, los cuales permiten generar limites y estabilidad del movimiento prismático del marcador con respecto al agujero de la conexión T. A partir de esta configuración, se tiene un posible deslizamiento del marcador de casi 2cm, lo cual se considera suficiente como margen de seguridad ante la presión generada. Así mismo como los empaques generan estabilidad y límites en el movimiento, se utilizan cauchos en el extremo opuesto a la punta del marcador para que siempre se ejerza una presión suficiente para que la punta del marcador esté lo más extendida posible sin dañarla. por último, para facilitar la conexión entre la T y el acople soporte-plato, se utiliza un segmento de tubo de PVC de 3/4'' de 33mm de largo conectado al orificio lateral.

Toda esta explicación se muestra en las siguientes imagenes:

Marcador con sus empaques:

![Marcador y empaques]()

Conexión T con segmento de PVC lateral:

![Conexión T con segmento de PVC lateral]()

Conjunto del soporte del amrcardor:

![Conjunto del soporte del amrcardor]()


***
## Acople soporte-plato

Ya teniendo el soporte del marcador, se diseña el acople entre dicho soporte y el plato del IRB140. Para empezar, cabe describir ambas conexiones.  

Por un lado, la conexión al soporte debe realizarse mediante una conexión hembra-macho, donde se tiene un diámetro interno del tubo de PVC de 21.4mm medido con un pie de rey. Por el otro lado, el plato cuenta con la siguiente disposición de agujeros roscados:

![Dimensiones del plato del IRB140](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/plato.png?raw=true)

### Modelado 3D

Con todo y lo anterior, se define la siguiente pieza para este acople:

![Modelo 3D soporte-plato](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/acople3D.png){width=250}

![Dimensiones del acople soporte-plato](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/base.png?raw=true)

Como se puede evidenciar, se cumplen las condiciones para el acople por tornillos M6 al plato, y una diferencia entre diámetros e 0.4mm entre la conexión macho-hembra, lo cual se contempló en caso de posibles imperfecciones en la impresión 3D.

### Impresión 3D

A partir de este modelado 3D, se utiliza el software Repetier Host y una impresora 3D para generar la pieza. Cabe resaltar que, al ser una impresora propia, la calidad no es tan alta como lo hubiera sido mandar a imprimir. Se imprime en PLA con capas de 0.3mm de espesor y densidad de pieza del 20%. Los resultados de la impresión se muestran a continuación:

![Modelo 3D en Repetier-Host]()

![Acople impreso]()

***
# Resultados finales de la herramienta

Con todo y lo anterior, se cuenta tanto con el soporte del marcador capaz de adaptar la punta del marcador a la superficie, y la base impresa en 3D para anclar la herramienta al plato del IRB140.

![Conjunto Separado Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/HfinalSeparada.jpg?raw=true)


Por último, se realiza el ajuste adecuado para que entre a presión la base de la herramienta con su conexión en T al enrollar la conexión macho con cinta de teflon. El resultado final se ve a continuación:
![Conjunto Unido Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/HfinalUnida.jpg?raw=true)

# Herramienta utilizada en RobotStudio
Ahora, para poder realizar una simulación adecuada en RobotStudio, es necesario tener el modelo de la herramienta lo más preisa posible, para esto, se generó en Inventor una pieza donde se tuviera tanto el marcador, soporte y acople, con el fin de definir el conjunto como herramienta de trabajo y definir adecuadamente el TCP. A continuación se muestra este modelo.


![Conjunto Unido Herramienta](https://github.com/jcaipap/Lab1_Robotica_Caipa_Holguin/blob/main/Dise%C3%B1o%20de%20la%20herramienta/Imagenes/HerrRS.png?raw=true)

