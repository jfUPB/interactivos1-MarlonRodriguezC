#### Codigo de p5.js


`````.js
let x = 200;
let y = 200;

function setup() {
  createCanvas(400, 400);
  
    
  myColour = color(random(255), random(255), random(255));


  background(myColour);

}

function draw() {
  // Update x and y randomly.
  
  circleColor = color(random(100, 256), random(100, 256), random(100, 256));
  strokeWeight(10);
  x += random(-10, 10);
  y += random(-10, 10);

  // Draw the point.
  point(x, y);
  Stroke(circleColor);
}
`````
El codigo para empezar le asigna las corrdenadas 200 en X  y 200 en Y para el inicio, despues crea una pantalla de 400 x 400 y crea un color al azar 
y luego se le da este color al azar al background, en l funcion draw, se crea tambien un color al azar para el punto que se movera por el espacio
y  hace que este se mueva de forma al azar entre -10 y 10 "espacios" y por ultimo se le asigna un color al azar

