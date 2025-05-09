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
let prevmicroBitAState = false;



var isDrawing = false; // <--- Nueva variable de control

function setup() {
  createCanvas(600, 600);
  colorMode(HSB, 360, 100, 100, 100);
  background(360);

  angle = getRandomAngle(direction);
  posX = floor(random(width));
  posY = 5;
  posXcross = posX;
  posYcross = posY;

  // Serial connection
  port = createSerial();
  connectBtn = createButton("Conectar micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(() => {
    if (!port.opened()) {
      port.open("MicroPython", 115200); // Sin argumentos
    } else {
      port.close();
    }
  });

  // Evento cuando llegan datos
  port.onReceive = serialEvent;

}

function serialEvent() {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length >= 1) {
      // Asume que el micro:bit manda algo como: x,y,true
      microBitAState = values[2].toLowerCase() === "true";

      if (microBitAState && !prevmicroBitAState) {
        isDrawing = true;
        print("Boton A presionado - dibujo activado");
      }

      prevmicroBitAState = microBitAState;
    }
  }
}

function draw() {
  if (!isDrawing) return; // <--- Si no está activado, no hace nada

  var speed = int(map(mouseX, 0, width, 0, 20));
  for (var i = 0; i <= speed; i++) {
    strokeWeight(1);
    stroke(180, 0, 0);
    point(posX, posY);

    posX += cos(radians(angle)) * stepSize;
    posY += sin(radians(angle)) * stepSize;

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
  
}

function getRandomAngle(currentDirection) {
  var a = (floor(random(-angleCount, angleCount)) + 0.5) * 90 / angleCount;
  if (currentDirection == NORTH) return a - 90;
  if (currentDirection == EAST) return a;
  if (currentDirection == SOUTH) return a + 90;
  if (currentDirection == WEST) return a + 180;
  return 0;
}
