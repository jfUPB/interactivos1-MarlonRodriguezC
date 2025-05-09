Bueno mi idea al inicio fue el crear dos ventanas de difernetes colores que al unirse entre si estas cambiasen de color 
como por ejemplo uno de color rojo y otro azul y al chocar entre si, estas daria su color morado, pero luego se me 
ocurrio una idea de cambiar los circulos por imagenes, lo hice  pero no cree una carpeta sprites ni nada, simplemente 
puse en views las imagenes y las use, pero me di cuenta que cuando mostraba la el otro gato desde una ventana, no veria
el gato de la otra ventana, veria el mismo gato de esa ventana.
Al dia siguiente se me ocurrio la idea de que cuando estos se juntasen (tuviesen un rango de distancia) podria el 
explorador abrir una pestan;a emergente con un video de estos gatos, aprovechadno que en el codigo pasado tuvimos
un ejercicio parecido y en el que con ayuda de la formula euclidiana se calculaba la distancia, aunque seguia con el
problema de que se repetia el gato en la ventana de este mismo gato, aunque usaba el let img2 y la usaba en el reload 
no terminaba funcionando, pero despues de consultar con IA ,resulto siendo que aunque si estaba por un buen camino, el 
codigo necesitaba calcular la ubicacion exacta del gato, no solo la ventana , por dar un ejemplo simple, de la ventana
1 a la 2 hay 500 de distancia, pero tambien se necsita la coordenada de donde esta el gato y entra el point1[0] con el 
point1[1, estos se suman a offset para tener la direccion exacta, aqui estan mis codigos 

### CODIGO PAGE1
``` js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point1 = [currentPageData.width / 2, currentPageData.height / 2];
let point2 = [0, 0];

let socket = io('http://localhost:3000');

socket.on('connect', () => {
    socket.emit('win1update', currentPageData);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
    point2 = [remotePageData.width / 2, remotePageData.height / 2];
});

let img1
let img2;

function preload() {
    img1 = loadImage('cat1.png'); // propio
    img2 = loadImage('cat2.png'); // remoto
}

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

    if (
        currentPageData.x !== previousPageData.x ||
        currentPageData.y !== previousPageData.y ||
        currentPageData.width !== previousPageData.width ||
        currentPageData.height !== previousPageData.height
    ) {
        point1 = [currentPageData.width / 2, currentPageData.height / 2];
        socket.emit('win1update', currentPageData);
        previousPageData = { ...currentPageData };
    }
}

let previousPageData = { ...currentPageData };
let linkOpened = false;
function draw() {
    background(255);
    checkWindowPosition();

    // Dibuja gato propio
    drawCircle(img1, point1[0], point1[1]);


    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);



    // Dibuja gato remoto
    let offsetX = remotePageData.x - currentPageData.x;
    let offsetY = remotePageData.y - currentPageData.y;
    let remoteX = offsetX + point2[0];
    let remoteY = offsetY + point2[1];

    let resultingVector = p5.Vector.sub(vector2, vector1);

    let distancia = resultingVector.mag();

    drawCircle(img2, remoteX, remoteY);
    if (distancia < 100 && !linkOpened) {

        window.open("https://www.tiktok.com/@silly_cat_q/video/7500721243767704887?_r=1&_t=ZS-8wAeelqa27O");
        linkOpened = true;
        }
    if (distancia >= 100) {
        linkOpened = false;
      }
    // Línea entre ambos
    stroke(50);
    strokeWeight(4);
    line(point1[0], point1[1], remoteX, remoteY);
}

function drawCircle(imageRef, x, y) {
    imageMode(CENTER);
    image(imageRef, x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```
#### CODIGO PAGE 2
``` js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let point1 = [0, 0];

let socket = io('http://localhost:3000');

socket.on('connect', () => {
    socket.emit('win2update', currentPageData);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
    point1 = [remotePageData.width / 2, remotePageData.height / 2];
});

let img1
let img2;

function preload() {
    img2 = loadImage('cat2.png'); // propio
    img1 = loadImage('cat1.png'); // remoto
}

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

    if (
        currentPageData.x !== previousPageData.x ||
        currentPageData.y !== previousPageData.y ||
        currentPageData.width !== previousPageData.width ||
        currentPageData.height !== previousPageData.height
    ) {
        point2 = [currentPageData.width / 2, currentPageData.height / 2];
        socket.emit('win2update', currentPageData);
        previousPageData = { ...currentPageData };
    }
}

let previousPageData = { ...currentPageData };

function draw() {
    background(255);
    checkWindowPosition();

    // Dibuja gato propio
    drawCircle(img2, point2[0], point2[1]);

    // Dibuja gato remoto
    let offsetX = remotePageData.x - currentPageData.x;
    let offsetY = remotePageData.y - currentPageData.y;
    let remoteX = offsetX + point1[0];
    let remoteY = offsetY + point1[1];

    drawCircle(img1, remoteX, remoteY);

    // Línea entre ambos
    stroke(50);
    strokeWeight(4);
    line(point2[0], point2[1], remoteX, remoteY);
}

function drawCircle(imageRef, x, y) {
    imageMode(CENTER);
    image(imageRef, x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

```
#### CODIGO DE SERVER

``` js

const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected');
    socket.on('disconnect', () => {
        console.log('User disconnected');
    });

    socket.on('win1update', (window1, sendid) => {
        page1 = window1;
        socket.broadcast.emit('getdata', page1);
    })

    socket.on('win2update', (window2, sendid) => {
        page2 = window2;
        socket.broadcast.emit('getdata', page2)
    })
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

Fue facil ? bueno pues aunque creo que me demore un poco mas a lo esperado, igualmente creo que fue un proyecto simple y estuve constantemente analizando el codigo y aprendi una o dos cosas de esto como el uso de URL externas o el procesamiento de dos imagenes en distintas ventanas ,se que se  puede lograr mas cosas en js y se puede agrandar el proyecto pero creo que es un buen proyecto para la unidad
