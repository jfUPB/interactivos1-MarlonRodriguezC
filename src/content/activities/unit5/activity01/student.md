#### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

El micro:bit y el p5.js se comunican en base a que el micro:bit envia cierta cantidad de informacion (coordenadas y botones) por medio de UART y el p5.js la recibe siempre y cuando se cumplan algunos parametros como que el micro:bit este conectado y envie 
los 4 datos pedidos, si este no esta conectado , el p5.js toma el estado del micro:bit como un estado de espera

#### ¿Cómo es la estructura del protocolo ASCII usado?

Es una estructura donde cada dato esta separado por comas y cuando acaba el mensaje  se acaba cuando el programador utiliza \n

#### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.

microBitConnected = true;
    connectBtn.html("Disconnect");
    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }

El codigo del micro:bit es tomado 
#### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?
#### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.
