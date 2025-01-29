``` js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
  
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  
    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
  
    let button = createButton('marlon');
    button.position(300, 300);
    button.mousePressed(sendBtnClick2);
}

function draw() {


    if (!port.opened()) 
    {
        connectBtn.html('Connect to micro:bit');
    } 
    else 
    {
        connectBtn.html('Disconnect');
    }
 }


function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendBtnClick() {
    port.write('h');
}
function sendBtnClick2(){
    port.write('j');
}
```

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
  
            if data[0] == ord('j'):
                display.show(Image.DUCK)
                sleep(400)
            if data[0] == ord('k'):
                display.show(Image.ANGRY)
                sleep(400)
            if data[0] == ord('l'):
                display.show(Image.SAD)
                sleep(400)

``` 
