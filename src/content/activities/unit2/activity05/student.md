
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();

    // Botón de conexión
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    // Botones para enviar caracteres
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
        port.open('MicroPython', 115200);  // Verifica el nombre exacto del puerto
        console.log('Puerto serie abierto');
    } else {
        port.close();
        console.log('Puerto serie cerrado');
    }
}

function sendBtnClick() {
    port.write('h');  // Enviar el carácter 'h'
    console.log('Enviando: h');  // Mostrar en la consola que se está enviando
}

function sendBtnClick2() {
    port.write('j');  // Enviar el carácter 'j'
    console.log('Enviando: j');
    
}

function sendBtnClick3() {
    port.write('k');  // Enviar el carácter 'k'
    console.log('Enviando: k');
}









from microbit import *

# Inicializa el puerto serie para recibir datos
uart.init(baudrate=115200, bits=8, parity=None, stop=2)

while True:
    if uart.any():  # Verifica si hay datos disponibles
        mensaje = uart.read()  # Lee los datos
        if mensaje:
            char = mensaje.decode('utf-8')  # Decodifica el mensaje como texto
            display.show(char)  # Muestra el carácter en la pantalla LED
            print('Recibido:', char)  # También imprime en el monitor serial de MicroPython
    else:
        display.clear()  # Si no hay datos, limpia la pantalla
    sleep(100)  # Pequeña pausa para evitar sobrecargar el procesador








