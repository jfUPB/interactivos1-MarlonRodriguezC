#### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Un protocolo es una area para recibir datos que se pueden tomar como diversas ordenes segun el programa

#### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Por un tema de organizacion de manera mas rapida y confiable y evitar errores, por ejemplo si estuviera programando en clave morse, seria una confusion
grande el poder ver que datos se estan recibiendo

#### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Para una forma de informar a la maquina "hasta aqui recibo datos" y procesar el mensaje

#### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
Para poder tener multiples tareas dentro del programa y que no sea todo de forma cronologica


#### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?

#### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?

#### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
``` python
if (port.availableBytes() > 0) {
    let data = port.readUntil("\n");
```

#### ¿Qué pasa si esto no se hace?

#### 8. ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
#### 9. Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
#### 10. Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
#### 11. Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
#### 12. ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
#### 13. ¿Qué aprendiste nuevo de p5.js que no sabías antes?
