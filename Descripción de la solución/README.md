# Descripcion de la solución

A pesar de tener los videos correspondientes de simulación y de implementación, se considera apropiado generar una descripción general de la solución realizada
***
## Simulación en RobotStudio


***
## Implementación

Para la etapa de implementación, ya teniendo una simulación bastante acorde al montaje físico en el Labsir, es relativamente sencillo realizar los pasos necesarios para completar la implementación.

Lo primero es configurar el IRB140 a partir del proyecto que realizamos importandolo mediante una USB. Una vez importado, es posible tener las rutinas de movimiento y la herramienta llamada ToolAJA, donde su modelado corresponde con la herramienta física que se monta en el plato del brazo. ahora, a pesar de que el simulador ya tiene en cuenta adecuadamente el las dimensiones del tablero inclinado, o el workobject, debido a la dificultad de posicionar el tablero tal cual como se hizo en RobotStudio, se redefine el sistema coordenado mediante el cálculo por 3 puntos del mismo, seleccionando en este orden sus extremos: Superior derecha, Superior izquierda, Inferior izquierda.

Ya teniendo las rutinas cargadas, y la herramienta y el workobject configurados adecuadamente, es posible empezar la rutina de dibujo de las iniciales "AJA".
