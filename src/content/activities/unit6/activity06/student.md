#### Describe con tus propias palabras cuál es la función del servidor Node.js en la arquitectura que exploramos. 
Para empezar lo usamos para la creacion de un servidor HTTP y dentro de este se utilizaran las variables globales page 1 y page 2 para el envio y recibimiento de informacion de parte de los dos clientes (nuestras dos ventanas) esto por medio de rutas de codigo, tambien toma encuenta si un cliente esta conectado o desconectado 
#### ¿Por qué los clientes p5.js no se comunican directamente entre sí?
El servidor facilita el reenviar la informacion si uno de los dos usuarios se conecta mas tarde que el otro y evita problemas de sincronizacion y es mas practico a la hora de obtener actualizada la informacion de los dos usuarios, taman;o, coordenadas, ID 

#### Explica la diferencia fundamental entre socket.emit() y socket.broadcast.emit() en el contexto de Socket.IO en el servidor.
el emit es para enviar datos a solo un usuario encambio el boradcast le envia a los demas conectados pero no al usuario de ese momento , y al io.emit es para todos incluyendo al usuario actual
#### ¿Cuándo usarías cada uno?
por ejemplo emit se envia cuando se necesita el propio ID  del usuario, el broadcast por ejemplo cuando un usuario se mueve y los demas lo tinen que ver

#### Compara la comunicación mediante Node.js/Socket.IO con la comunicación serial (ASCII y binaria con framing) que viste en unidades anteriores.
#### Menciona al menos una ventaja y una desventaja de cada enfoque según el contexto de aplicación (ej. conectar micro:bit vs. conectar dos navegadores).

-Una ventaja del conectar el micro:bit al pc es que no es necesario crear un servidor y un HTTP para que este pueda interactuar con la pantalla, y una desventaja es que no es tan "portatil" por asi decirlo, tipo seria necesario comprar o tener un micro:bit para esta clase de experimentos encambio con la comunicacion serial se podria hacer desde cualquier computadora actual

-Una ventaja de la creacion mediante Node.Js es que se puede modificar las paginas siempre y cuando el servidor este en funcionamiento, sin tener que parar todo, como ocurre con microbit, simplemente se guarda el archivo y se reinicia la pagina y podemos notar el cambio, y una desventaja podria ser menos "interactivo" en mi opinion al no tener algo fisico con lo que interactuar y seguir con limitaciones a las pantallas

¿Qué rol juega el protocolo http y qué rol juega socket.io (que usa WebSockets por debajo) en la aplicación del caso de estudio?
Dando un ejemplo, http es la cual lleva todo lo que tiene pagina como el html o el css, como si fuera un telefono fijo antiguo, en este caso seria el disen;o del telefono, las teclas y demas cosas necesarias, y el  socket.io es la linea con la cual te comunicas en este telefono, enviando y recibiendo mensajes 


¿Qué fue lo más sorprendente o interesante que aprendiste sobre la comunicación en red en esta unidad? diria que lo mas sorprendete fue el uso del servidor dentro del node.js creeria que es una forma simple para empezar en el tema de los servidores y la facilidad de poder hacer uno dentro de la computadora
