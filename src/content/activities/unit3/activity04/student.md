#### p5.js recibe los mensajes del puerto serial
utilizando el codigo pasado de la bomba 

let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
  
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 80);
    connectBtn.mousePressed(connectBtnClick);
  
    let sendBtnA = createButton('envia A');
    sendBtnA.position(80, 150);
    sendBtnA.mousePressed(sendBtnAClick);
  
    let sendBtnB = createButton('envia B');
    sendBtnB.position(80, 180);
    sendBtnB.mousePressed(sendBtnBClick);
  
    let sendBtnS = createButton('Shake');
    sendBtnS.position(80, 220);
    sendBtnS.mousePressed(sendBtnSClick);
  
    let sendBtnT = createButton('logo');
    sendBtnT.position(80, 250);
    sendBtnT.mousePressed(sendBtnTClick);
}

function draw() {
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
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

function sendBtnAClick() {
    port.write('A');  // Comando para incrementar el tiempo
}

function sendBtnBClick() {
    port.write('B');  // Comando para disminuir el tiempo
}

function sendBtnSClick() {
    port.write('S');  // Comando para iniciar o detener el temporizador
}

function sendBtnTClick() {
    port.write('T');  // Comando para tocar el logo
}
