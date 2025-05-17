
1. Si, nos da un error ‘net::ERR_CONNECTION_REFUSED’ y se refiere a un error al no recibir el socket , si al reiniciar el servidor este funciona

2. Al principio no obtenía la información correcta para conectarse con el page2, aquí confirmo la importancia de enviar el estado inicial apenas conectarse 

3. En la consola de page 2 al moverse no tendrá ningún comentario, pero al mover page 2, este si mostrara el comentario. Por que si y por que no?por que utiliza el remotePageData en el código y este y se toma la información de la otra ventana con Data Window, si fuese al contrario entonces al mover la page 2, dentro de la consola de page 1, podremos ver los datos
4. Esta tónica es eficiente ya que para empezar lleva un registro exacto de las acciones llevadas acabo y de forma “resumida” sin tener que repetir un mensaje 30 veces el cual es la misma acción 

``` js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight

}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let socket = io('http://localhost:3000')

socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win2update', currentPageData, socket.id);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
    console.log(remotePageData);
});


let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};


function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}


function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y ||
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {


        console.log("Page 2 detected change, sending update:", currentPageData); // Log para saber cuándo enviamos
        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}


function draw() {


    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);

    let distancia = resultingVector.mag();
    background(map(distancia, 0, 1000, 255, 0));

    let size = map(remotePageData.width, 100, 1920, 50, 300); // Ajusta los valores si es necesario
    drawCircle(point2[0], point2[1], size);

    checkWindowPosition();

    stroke(50)
    strokeWeight(20)
    if (resultingVector.x < 0) {
       stroke(0,0,255)
     } else {
        stroke(0,20,0)
     }
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2)
    line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2)

}

function drawCircle(x, y, size) {
    fill(255, 0, 0);
    ellipse(x, y, size, size); // <-- tamaño variable
}


function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```
