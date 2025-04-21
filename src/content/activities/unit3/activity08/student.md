#### Codigo en python
``` python
from microbit import *

uart.init(baudrate=115200)

display.show(Image.BUTTERFLY)

while True:
    if button_a.was_pressed():
        uart.write('A')
    if button_b.was_pressed():
        uart.write('B')
    if accelerometer.was_gesture('shake'):
        uart.write('S')
    if pin_logo.is_touched():
        uart.write('T')
        sleep(500)
```



#### Codigo en micro:bit 




``` Js
let estado = "Configuracion";
let duracion = 20;
let intento = "";
let intervalo;

let port;
let connectBtn;

function setup() {
  createCanvas(400, 400);
  background(220);
  textSize(20);

  port = createSerial();

  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 80);
  connectBtn.mousePressed(connectBtnClick);

  sendBtnA = createButton("envia A");
  sendBtnA.position(80, 150);
  sendBtnA.mousePressed(() => manejarEvento("A"));

  sendBtnB = createButton("envia B");
  sendBtnB.position(80, 180);
  sendBtnB.mousePressed(() => manejarEvento("B"));

  sendBtnS = createButton("Shake");
  sendBtnS.position(80, 220);
  sendBtnS.mousePressed(() => manejarEvento("S"));

  sendBtnT = createButton("logo");
  sendBtnT.position(80, 250);
  sendBtnT.mousePressed(() => manejarEvento("T"));
}

function draw() {
  background(220);

  // Controlar los datos del serial
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      
      if (dataRx == "A") {
        manejarEvento("A");
      } else if (dataRx == "B") {
        manejarEvento("B");
      }
      else if (dataRx == "S") {
        manejarEvento("S");
      }
      else if (dataRx == "T") {
        manejarEvento("T");
      }
    }
  }

  // UI de la bomba
  fill(0);
  if (estado === "Explosion") {
    text("Exploto", 180, 200);
  } else if (estado === "Armado") {
    text(`Tiempo: ${duracion}`, 180, 200);
    text(`Clave: ${intento}`, 180, 220);
  } else if (estado === "Configuracion") {
    text(`Duración: ${duracion}`, 180, 200);
  }
}

function manejarEvento(evento) {
  if (estado === "Configuracion") {
    if (evento === "A" && duracion < 61) {
      duracion++;
    } else if (evento === "B" && duracion > 10) {
      duracion--;
    } else if (evento === "S") {
      estado = "Armado";
      intento = "";
      startCuentaRegresiva();
    }
  } else if (estado === "Armado") {
    if (evento === "A") {
      if (intento === "") {
        intento = "A";
      } else if (intento === "AB") {
        intento = "ABC";
      } else {
        intento = "";
      }
    } else if (evento === "B") {
      if (intento === "A") {
        intento += "B";
      } else {
        intento = "";
      }
    } else if (evento === "S") {
      if (intento === "ABC") {
        detenerCuentaRegresiva();
        estado = "Configuracion";
        duracion = 20;
        intento = "";
      } else {
        intento = "";
      }
    }
  } else if (estado === "Explosion") {
    if (evento === "T") {
      estado = "Configuracion";
      duracion = 20;
    }
  }
}

function startCuentaRegresiva() {
  intervalo = setInterval(() => {
    duracion--;
    if (duracion <= 0) {
      clearInterval(intervalo);
      estado = "Explosion";
    }
  }, 1000);
}

function detenerCuentaRegresiva() {
  clearInterval(intervalo);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}
``` 
