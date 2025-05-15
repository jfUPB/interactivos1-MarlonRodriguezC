#### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
-

#### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?

Por un tema de organizacion de manera mas rapida y confiable y evitar errores y poder dar diversos mensajes en solo una cadena de texto, como vimos al tener que enviar 4 mensajes al mismo tiempo, dos posiciones y dos booleanos

#### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Para una forma de informar a la maquina "hasta aqui recibo datos" y procesar el mensaje, algo asi como un limite

#### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
Para poder tener multiples tareas dentro del programa y que no sea todo de forma cronologica 

#### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
-

#### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?

Significa que pasa las letras y demas caracteres a numeros, estos numeros dependen de como este formulado en la tabla ASCII 

#### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
``` python
if (port.availableBytes() > 0) {
    let data = port.readUntil("\n");
```
para verificar que el mensaje esta completo 

#### ¿Qué pasa si esto no se hace?

muy probablemente estaria leyendo mensajes vacios y generaria errores al ver que no hay ningun mensaje

#### 8. ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
-
#### 9. Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
yo usaria la coma para dividir la informacion pero para usar los espacios diria que usaria el comando data.split(" ")

#### 10. Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
-

#### 11. Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial? 
segun la pagina "https://onlinestringtools.com/convert-string-to-ascii" al pasar estos datos (123,756,False,True) a hexadecimal nos pone  31 32 33 2c 37 35 36 2c 46 61 6c 73 65 2c 54 72 75 65

#### 12. ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
El envio y recepcion de datos por el puerto serial

#### 13. ¿Qué aprendiste nuevo de p5.js que no sabías antes?
-
