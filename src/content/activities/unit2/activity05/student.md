#### Solucion
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
    sendBtn.position(220, 100);
    sendBtn.mousePressed(sendBtnClick);

    let sendBtn2 = createButton('Send Hate');
    sendBtn2.position(120, 200);
    sendBtn2.mousePressed(sendBtnClick2);

    let sendBtn3 = createButton('Send Marlon');
    sendBtn3.position(300, 300);
    sendBtn3.mousePressed(sendBtnClick3); 

    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
        console.log('Puerto serie abierto');
    } else {
        port.close();
        console.log('Puerto serie cerrado');
    }
}

function sendBtnClick() {
    port.write('h');  // Enviar el carácter 'h'
    console.log('Enviando: h'); 
}

function sendBtnClick2() {
    port.write('j'); 
    console.log('Enviando: j');
    
}

function sendBtnClick3() {
    port.write('k');
    console.log('Enviando: k');
}
```

El codigo dentro p5.js se creo teniendo encuenta las actividades pasadas, se crearon los botones y se creo un una letra para cada una, dentro de micro:bit la idea principal es que dependiendo del char que se envie al presionar el boton, este este constantemente en un while para saber si se esta enviando datos, este  lea el char que se esta enviando y lo muestre en la pantalla LED (DATO: se puede borrar el char que se muestra en pantalla si se pone un display.clear al momento de dejar de enviar el mensaje, pero lo deje permanente en la pantalla hasta recibir algun cambio para confirmar su funcionamiento)



``` js

from microbit import *

# Inicializa el puerto serie para recibir datos
uart.init(baudrate=115200, bits=8, parity=None, stop=2)

while True:
    if uart.any(): 
        mensaje = uart.read()  # Lee los datos
        if mensaje:
            char = mensaje.decode('utf-8') 
            display.show(char)  # Muestra el carácter en la pantalla LED
            print('Recibido:', char)  # También imprime en el monitor serial de MicroPython

```







