#### Circulo moviendose en el eje X 

Tome el codigo ya visto en micro:bit para asigar los botones como A y B
``` js
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)
                sleep(500)
                display.show(Image.HAPPY)
```
Lo coonecte al html de p5.js con el codigo
``` js
<script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
```

Para el siguiente codigo en P5.js 
``` js

let port;
let connectBtn;


var circleX = 200;
var circleY = 200;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    

}

function draw() {

    ellipse(circleX, circleY, 50, 50);
  
    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
       
   if(dataRx == 'B'){
             circleX +=5;    
        }
   
     
  else if (dataRx == 'A')
   {
     circleX -= 5;
   }


    if (!port.opened()) 
    {
        connectBtn.html('Connect to micro:bit');
    } 
    else 
    {
        connectBtn.html('Disconnect');
    }
  } 
}


  

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}
```
se declara la poscion del circulo de 200 y 200  y se declara el boton para conectar el microbit y se crea una elipse que aparecera en la posicion ya especificada, para la funcion draw toma un IF se preciona el boton A o B se le sumara o restara 5 a la posicion del circulo y asi haciendo que se mueva 
![Resultado del programa](../../../../assets/un1-ac11.jpeg)
