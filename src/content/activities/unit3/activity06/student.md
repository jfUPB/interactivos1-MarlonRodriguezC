#### Tabla con todos los vectores posibles

!(../../../../assets/unidad3-act6)


#### Codigo de micropython
``` python
from microbit import *
import utime
import music

# Variables globales para los eventos
evento = None
evento_ocurrido = False

class Bomba:
    def __init__(self):
        self.duracion = 20
        self.state = 'Configuracion'
        self.start_time = 0
        display.scroll(self.duracion)
        self.intento = ""   # Variable para almacenar la secuencia de claves

    def reset_secuencia(self):
        self.intento = ""
    
    def update(self):
        global evento, evento_ocurrido

        if self.state == 'Configuracion':
            display.scroll(self.duracion)
            if evento_ocurrido:
                if evento == 'A' and self.duracion < 61:
                    self.duracion += 1 
                    display.scroll(self.duracion)
                elif evento == 'B' and self.duracion > 9:
                    self.duracion -= 1
                    display.scroll(self.duracion)
                elif evento == 'S':
                    display.scroll('Armada')
                    self.start_time = utime.ticks_ms()
                    self.state = 'Armado'
                    self.reset_secuencia()  
                evento_ocurrido = False

        elif self.state == 'Armado':
         
            if utime.ticks_diff(utime.ticks_ms(), self.start_time) > 1000:
                self.start_time = utime.ticks_ms()
                self.duracion -= 1
                display.scroll(self.duracion)
                if self.duracion == 0:
                    music.play(music.NYAN)
                    display.show(Image.SKULL)
                    self.state = 'Explosion'

          
            if evento_ocurrido:
                
                if evento == 'A':
                   
                    if self.intento == "":
                        self.intento = "A"
                        display.scroll('A')
                  
                    elif self.intento == "AB":
                        self.intento = "ABC"
                        display.scroll('C')
                        
                    else:
                        display.scroll('Reinicio')
                        self.reset_secuencia()
                        
                elif evento == 'B':
                   
                    if self.intento == "A":
                        self.intento += "B"  
                        display.scroll('B')
                    else:
                        display.scroll('Reinicio')
                        self.reset_secuencia()
                        
                elif evento == 'S':
                  
                    if self.intento == "ABC":
                        display.scroll('Desarmada')
                        self.duracion = 20
                        self.state = 'Configuracion'
                    else:
                        display.scroll('Reinicio')
                        self.reset_secuencia()
                        
                evento_ocurrido = False

        elif self.state == 'Explosion':
            if pin_logo.is_touched():
                self.duracion = 20
                display.scroll(self.duracion)
                self.state = 'Configuracion'
            if evento == 'T':
                self.duracion = 20
                display.scroll(self.duracion)
                self.state = 'Configuracion'

def tareaEventos():
    global evento, evento_ocurrido

    if button_a.was_pressed():
        evento = 'A'
        evento_ocurrido = True
    elif button_b.was_pressed():
        evento = 'B'
        evento_ocurrido = True
    elif accelerometer.was_gesture('shake'):
        evento = 'S'
        evento_ocurrido = True
    elif pin_logo.is_touched():
        evento = 'T'
        evento_ocurrido = True
    elif uart.any():
        mensaje = uart.read(1)
        if mensaje is not None:
            mensaje = mensaje.decode('utf-8')
            if mensaje in ['A', 'B', 'S', 'T']:
                evento = mensaje
                evento_ocurrido = True

def tareaBomba():
    bomba.update()

bomba = Bomba()

while True:
    tareaEventos()  # Leer eventos
    tareaBomba()    # Actualizar la bomba con los eventos


```
#### Codigo de p5.js
``` js

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
``` 
