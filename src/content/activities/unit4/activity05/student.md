Para empezar me guie por este proyecto: http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_2_01 el cual es una simulacion que empieza con solo darle click al inicio, que quiero yo? que al darle click al boton A de microbit, esta inicie aqui dejo el codgio inicial: 

```Js
'use strict';

var NORTH = 0;
var EAST = 1;
var SOUTH = 2;
var WEST = 3;
var direction = SOUTH;

var stepSize = 3;
var minLength = 10;
var diameter = 1;
var angleCount = 7;
var angle;
var reachedBorder = false;

var posX;
var posY;
var posXcross;
var posYcross;

function setup() {
  createCanvas(600, 600);
  colorMode(HSB, 360, 100, 100, 100);
  background(360);

  angle = getRandomAngle(direction);
  posX = floor(random(width));
  posY = 5;
  posXcross = posX;
  posYcross = posY;
}

function draw() {
  var speed = int(map(mouseX, 0, width, 0, 20));
  for (var i = 0; i <= speed; i++) {

    // ------ draw dot at current position ------
    strokeWeight(1);
    stroke(180, 0, 0);
    point(posX, posY);

    // ------ make step ------
    posX += cos(radians(angle)) * stepSize;
    posY += sin(radians(angle)) * stepSize;

    // ------ check if agent is near one of the display borders ------
    reachedBorder = false;

    if (posY <= 5) {
      direction = SOUTH;
      reachedBorder = true;
    } else if (posX >= width - 5) {
      direction = WEST;
      reachedBorder = true;
    } else if (posY >= height - 5) {
      direction = NORTH;
      reachedBorder = true;
    } else if (posX <= 5) {
      direction = EAST;
      reachedBorder = true;
    }

    // ------ if agent is crossing his path or border was reached ------
    loadPixels();
    var currentPixel = get(floor(posX), floor(posY));
    if (
      reachedBorder ||
      (currentPixel[0] != 255 && currentPixel[1] != 255 && currentPixel[2] != 255)
    ) {
      angle = getRandomAngle(direction);

      var distance = dist(posX, posY, posXcross, posYcross);
      if (distance >= minLength) {
        strokeWeight(3);
        stroke(0, 0, 0);
        line(posX, posY, posXcross, posYcross);
      }

      posXcross = posX;
      posYcross = posY;
    }
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(360);
}

function getRandomAngle(currentDirection) {
  var a = (floor(random(-angleCount, angleCount)) + 0.5) * 90 / angleCount;
  if (currentDirection == NORTH) return a - 90;
  if (currentDirection == EAST) return a;
  if (currentDirection == SOUTH) return a + 90;
  if (currentDirection == WEST) return a + 180;
  return 0;
}
```
Dentro de micropython ejecute el codigo del enunciado, aunque sabia que no necesitaria el acelerometro 

```Python
# Imports go at the top
from microbit import *

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed() 
    bState = button_b.is_pressed()
    data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
    uart.write(data)
    sleep(100) # Envia datos a 10 Hz

```
Y de paso utilize el html ya usado en la actividad pasada para conectar el p5.js con mi micro:bit 
``` html
<!DOCTYPE html>
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/p5/lib/p5.min.js"></script>
    <script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <script src="sketch.js"></script>
  </body>
</html>
```
Ya con todo preparado  comenze a cambiar algunas cosas dentro del codigo, como por ejemplo an;adirle su opcion de Connect micro:bit (estas no fueron necesarias crearlas desde 0, ya en anteriores unidades ya se mostraba su procedimiento y creacion) y se crea 3 variable snuevas, un booleano para saber si estaba dibujando y otros dos para saber el estado del boton A y su estado anterior , y se hace dos condicionales nuevo, uno donde pregunta si se esta presionando el boton el cual crea un true dentro del booleano, y el otro (el cual usa el booleano) para ejecutar la accion for de dibujo del programa. Como mencione antes en este programa no se necesita todas las herramientas del micro:bit por tanto solo se uso "microBitAState" a la hora de recibir los 4 datos dentro del proyecto, se que se puede simplicar mas pero para este tipo de simulacion no se necesita los acelerometros (ya antes dicho)
```Js
'use strict';

var NORTH = 0;
var EAST = 1;
var SOUTH = 2;
var WEST = 3;
var direction = SOUTH;

var stepSize = 3;
var minLength = 10;
var diameter = 1;
var angleCount = 7;
var angle;
var reachedBorder = false;

var posX;
var posY;
var posXcross;
var posYcross;

let port;
let connectBtn;
let microBitConnected = false;

let microBitAState = false;
let prevMicroBitAState = false;

let estaDibujando = false;

function setup() {
  createCanvas(600, 600);
  colorMode(HSB, 360, 100, 100, 100);
  background(360);

  angle = getRandomAngle(direction);
  posX = floor(random(width));
  posY = 5;
  posXcross = posX;
  posYcross = posY;

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(() => {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
    } else {
      port.close();
    }
  });
}

function draw() {
  var speed = int(map(mouseX, 0, width, 0, 20));

  if (!port.opened()) {
    microBitConnected = false;
    connectBtn.html("Connect to micro:bit");
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length === 4) {
          microBitAState = values[2] === "True" || values[2] === "true";
        }
      }
    }
  }

 
  if (microBitConnected && microBitAState && !prevMicroBitAState) {
    estaDibujando = true;
  }
  if (!microBitAState) {
    estaDibujando = false;
  }

  prevMicroBitAState = microBitAState;

  if (estaDibujando) {
    for (var i = 0; i <= speed; i++) {
      // ------ draw dot at current position ------
      strokeWeight(1);
      stroke(180, 0, 0);
      point(posX, posY);

      // ------ make step ------
      posX += cos(radians(angle)) * stepSize;
      posY += sin(radians(angle)) * stepSize;

      // ------ check if agent is near one of the display borders ------
      reachedBorder = false;

      if (posY <= 5) {
        direction = SOUTH;
        reachedBorder = true;
      } else if (posX >= width - 5) {
        direction = WEST;
        reachedBorder = true;
      } else if (posY >= height - 5) {
        direction = NORTH;
        reachedBorder = true;
      } else if (posX <= 5) {
        direction = EAST;
        reachedBorder = true;
      }

      // ------ if agent is crossing his path or border was reached ------
      loadPixels();
      var currentPixel = get(floor(posX), floor(posY));
      if (
        reachedBorder ||
        (currentPixel[0] != 255 && currentPixel[1] != 255 && currentPixel[2] != 255)
      ) {
        angle = getRandomAngle(direction);

        var distance = dist(posX, posY, posXcross, posYcross);
        if (distance >= minLength) {
          strokeWeight(3);
          stroke(0, 0, 0);
          line(posX, posY, posXcross, posYcross);
        }

        posXcross = posX;
        posYcross = posY;
      }
    }
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(360);
}

function getRandomAngle(currentDirection) {
  var a = (floor(random(-angleCount, angleCount)) + 0.5) * 90 / angleCount;
  if (currentDirection == NORTH) return a - 90;
  if (currentDirection == EAST) return a;
  if (currentDirection == SOUTH) return a + 90;
  if (currentDirection == WEST) return a + 180;
  return 0;
}
```
