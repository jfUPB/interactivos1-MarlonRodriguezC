https://openprocessing.org/sketch/1297448

Es una simulación de partículas de tinta, puedes “dibujar” y ensuciar la pantalla dándole un estilo del uso de una tinta donde si lo dejas mucho tiempo presionando encima, la tinta dejara una mancha mucho mas negra

¿Qué técnicas utiliza? 

Para empezar una función para crear un background del tamaño de la pantalla  y otra función que utiliza  un condicional if para saber si el mouse está siendo presionado y este crea un ‘new’ de ‘particle’ y dentro de la misma función hace un ciclo donde se actualiza constantemente en un update la pantalla y muestra las partículas y elimina las ‘partículas muertas’.

Después nos muestra la clase particle la cual dentro de ‘constructor’ se inicializa algunos datos como locación, velocidad, aceleración y demás. Dentro de ‘update()’ es donde se utiliza esta información, haciendo que la aceleración empiece en 0  y usando el ‘noise’ para el movimiento y locación de las partículas  y por último muestra estas partículas con un show() y este mismo es el que también configura el color de la tinta con el ‘fill’

mi version: https://editor.p5js.org/mugsky/sketches/G1VZHSkOc

que cambios hize? aumente el tamaño de las particulas y dandoles mas velocidad y que tuviesen diferentes colores
____________________________________________________________
http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_2_01
Este diseño generativo hará una serie de líneas que aparecerán automáticamente en la pantalla, se cruzara con otras creando triángulos y cuadrados y seguirá dibujando hasta dentro de estas figuras haciendo que la pantalla pase de ser totalmente blanca a negra con unos pocos pixels negros

¿Qué técnicas utiliza? 

Para empezar utiliza variables donde recoge el este, oeste, norte y sur, y angulos, asi tambien el diametro y largo de las líneas y dentro de su setup toma de forma al azar su ángulo con la función  ‘getRandomAngle’ la cual según sea su dirección cardinal sumara o restara su ángulo (por cierto hay otra función la cual se encarga de crear un screenshot con la tecla s) , volviendo al código se utiliza una función draw() para trazar estas líneas y chequear que cuando estas estén cerca a los bordes de la pantalla este cambie de dirección cardinal, si este llegase a pasar los límites, el trazo vuelve desde 0 

mi version: https://editor.p5js.org/mugsky/sketches/Cmd40YPRv

que hice? ahora la pantalla  SI o SI empieza desde arriba y choca un par de veces choca entre las pared ‘sur’ de la pantalla, después de eso entra en un bucle entre las pantallas de los lados, aunque puede durar poco o mucho para liberarse de este ciclo, estos dos pasos iniciales (primero vertical y luego horizontal) se repetirán cada que inicia el programa
____________________________________________________________
 https://p5js.org/examples/3d-orbit-control/
Dentro de este se orbita dentro un objeto 3d, una esfera creada por cubos y lo que parece ser dos cilindros modelados en forma de estrella para ser la cabeza y cola de la esfera


¿Qué técnicas utiliza? 

Para empezar creando el canvas este utiliza un WEBGL lo cual utiliza tareas de renderizado y shaders de uso 3D y crea el trazo, despues utiliza un orbitControl() para orbitar en el area, y con ayuda de ‘for’s se crea la esfera la cual va cambiando el angulo X o Z segun tenga los 180 o 360 grados, ya lo ultimo le indica al programa que giren alrededor del  centro de la esfera y usa un translate, encuanto espacio de estos cubos, entre menos espacio, mas cerca estaran unos de otros

mi version: https://editor.p5js.org/mugsky/sketches/VjrT4eGlj

que hice? la esfera es más pequeña y cada que inicie su color cambiará , tambien le cambio su trazo por uno más grande , ahora parece una figura 2d aunque aun se puede rotar en el espacio
