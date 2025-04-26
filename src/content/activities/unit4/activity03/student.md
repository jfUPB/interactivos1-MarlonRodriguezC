Caso de estudio: micro:bit
Desde esta actividad hasta la fase de aplicación, te voy a guiar para que transformes y adaptes el caso de estudio para lograr controlar partes de este con el micro:bit. Primero te mostraré cómo transmitir información desde el micro:bit.

🎯 Enunciado: analiza el código del micro:bit que te permitirá enviar información a un sketch en p5.js.

Vas a analizar lentamente el siguiente código del micro:bit

# Imports go at the top
from microbit import *

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed() 
    bState = button_b.is_pressed()
    data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
    uart.write(data)
    sleep(100) # Envia datos a 10 Hz
Programa el micro:bit con este código y luego abre la aplicación SerialTerminal para ver los datos que se están enviando.

### ¿Qué información se está enviando? ¿Cómo se está enviando? Qué significa esta parte del código:
"{},{},{},{}\n".format(xValue, yValue, aState,bState)

Esto significa que dentro de estas capsulas estara la informacion del valor de x, y y el estado de los botnes

#### ¿Qué puedes inferir de la estructura de los datos?
Se estan actualizando constantemente, se toma las coordenas del acelerometro ya ejecutado en el codigo y alerta el uso de los botones pasando los bools de false a true y vicebersa

#### ¿Por qué se separan los datos con comas y se termina con un salto de línea?
porque en el codigo   "{},{},{},{}\n".format(xValue, yValue, aState,bState)" se muestra en forma de separar palabras, numeros, datos y el salto de linea para mejor orden a la escribir en el serial 

#### ¿Qué crees que pasaría si no se separan los datos con comas y no terminan con un salto de línea?
los datos se verian unos encima de otros y podria dar confusiones 
#### Para qué crees que se usa la función sleep(100)? ¿Qué pasaría si no se usara?
Es un  espera tiempo de esperar para repetir el bucle, no se daria la espera y se repetiria al milisegunda que temrino

#### Observa cómo cambian los valores de xValue y yValue a medida que el micro:bit se inclina hacia la izquierda, derecha, adelante y atrás. ¿Qué valores toman xValue y yValue en cada caso?
X es para derecha y izquierda y Y es para adelante y atras

#### ¿Qué valores toman aState y bState cuando presionas los botones A y B?
True 
#### Observa qué ocurre si en vez de is_pressed() usas was_pressed(). ¿Qué diferencias encuentras?
la casilla 3 se pondra en modo 'true' si A es presionado, y si es B sera la casilla 4

Finalmente, analiza este asunto: si el micro:bit tiene los siguientes datos xValue: 969, yValue: 652, aState: True, bState: False ¿Qué bytes se enviarían por el puerto serial? Piensa, primero piensa por favor, y luego verifica con la aplicación SerialTerminal. Ten presente que en Mostrar datos como puedes ver los bytes que se están enviando mediante Todo en HEX.

Si se tuviese que crear dentro de la pagina las coordenadas exactas se deberia mirar print por print para hayarlo, pero sabiendo que es HEX, se puede usar un convertidor de texto a HEX, por ejemplo usando esta pagina "https://magictool.ai/tool/text-to-hex-converter/es/" se puede saber que es '3936392c3635322c547275652c46616c7365'

