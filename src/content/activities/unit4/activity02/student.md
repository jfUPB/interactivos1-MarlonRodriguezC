####  Solucion
``` Js
var c;
var lineModuleSize = 0;
var angle = 0;
var angleSpeed = 1;
var lineModule = [];
var lineModuleIndex = 0;
var clickPosX = 0;
var clickPosY = 0;

#### Se inicializan las variable y se crea un arreglo


``` Js
function preload() {
  lineModule[1] = loadImage('data/02.svg');
  lineModule[2] = loadImage('data/03.svg');
  lineModule[3] = loadImage('data/04.svg');
  lineModule[4] = loadImage('data/05.svg');
}
``` 
#### Los arreglos guardan dentro de  la carpeta data, unas "brochas" para el uso del programa

``` Js
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);
  //cursor(CROSS);
  noCursor();
  strokeWeight(0.75);

  c = color(181, 157, 0);
}
``` 
#### Se le especifica al programa que no se mostrara un cursos y como sera su fondo, asi tambien el color con el que se inicara a pintar

``` Js
function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
``` 
#### Se ajusta el canvas segun la pantalla del usuario
``` Js
function draw() {
  if (mouseIsPressed && mouseButton == LEFT) {
    var x = mouseX;
    var y = mouseY;
    if (keyIsPressed && keyCode == SHIFT) {
      if (abs(clickPosX - x) > abs(clickPosY - y)) {
        y = clickPosY;
      } else {
        x = clickPosX;
      }
    }
``` 
#### Dentro de estas funciones se utiliza por ejemplo el SHIFT para crear circulos perfectos y no 'desviarse'
``` Js
    push();
    translate(x, y);
    rotate(radians(angle));
    if (lineModuleIndex != 0) {
      tint(c);
      image(lineModule[lineModuleIndex], 0, 0, lineModuleSize, lineModuleSize);
    } else {
      stroke(c);
      line(0, 0, lineModuleSize, lineModuleSize);
    }
    angle += angleSpeed;
    pop();
  }
}
``` 
#### Se utiliza translate y rotate para el movimeinto del punto del raton, se toma dos condicionales, si  esta es distinta a 0 (una trazo comoun) 
dibuajara con una de las opciones escojidas ara el arrego, si no esta se mantendra dibujando un trao comun
``` Js
function mousePressed() {
  // create a new random color and line length
  lineModuleSize = random(50, 160);

  // remember click position
  clickPosX = mouseX;
  clickPosY = mouseY;
}
``` 
#### Si el mouse esta siento presionado este cada que se vuelva a presionar tendra un taman;o al azar
``` Js
function keyPressed() {
  if (keyCode == UP_ARROW) lineModuleSize += 5;
  if (keyCode == DOWN_ARROW) lineModuleSize -= 5;
  if (keyCode == LEFT_ARROW) angleSpeed -= 0.5;
  if (keyCode == RIGHT_ARROW) angleSpeed += 0.5;
  
}
``` 
#### Utilizando las flechas del tclado se puede  modificar la velocidad y el angulo al que giran
``` Js
function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);
``` 
#### Esto crea la opcion de hacer screenshoots
``` Js

  // reverse direction and mirror angle
  if (key == 'd' || key == 'D') {
    angle += 180;
    angleSpeed *= -1;
  }
``` 
#### Esto puede darle la vuelta de 180 grados  al trazo segun la posicion que este
``` Js
  // change color
  if (key == ' ') c = color(random(255), random(255), random(255), random(80, 100));
  // default colors from 1 to 4
  if (key == '1') c = color(181, 157, 0);
  if (key == '2') c = color(0, 130, 164);
  if (key == '3') c = color(87, 35, 129);
  if (key == '4') c = color(197, 0, 123);

  // 
  if (key == '5') lineModuleIndex = 0;
  if (key == '6') lineModuleIndex = 1;
  if (key == '7') lineModuleIndex = 2;
  if (key == '8') lineModuleIndex = 3;
  if (key == '9') lineModuleIndex = 4;
}
``` 
#### Estas opciones del 1 al 6 logran cambiar el color del trazo y del 5 al 9 se utiliza el arreglo ya creado al inicio del programa para sus guardar las imagenes las cuales se pueden usar como"brochas"


### me FALTAN SUBIR LAS IMAGENES
