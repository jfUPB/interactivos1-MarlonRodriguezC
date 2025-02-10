Manipulando Entradas Digitales
Enunciado: realiza experimentos para leer los estados de los botones A y B, y el botón virtual del logo del micro:bit. ¿Cómo harás estos experimentos? Como ya viste la documentación vas a realizarte esta pregunta: 
¿Qué pasará si hago esto? para responder esta pregunta pensarás qué puedes hacer para responderla (experimento), luego lanzarás una hipótesis (reflexionarás y pensarás que crees que pasará), posteriormente realizarás 
el experimento, analizarás los resultados explicando por qué ocurre lo que observas y finalmente concluirás.

Entrega: para cada experimento

¿Qué querías comprobar?
¿Cuál fue tu hipótesis?
Los códigos involucrados en el experimento
Descripción de lo resultados
Análisis de esos resultados
Conclusiones

#### Que quiero comprobar?
Es posible hacer una accion con la condicion de presionar A y B al mismo tiempo?
#### Hipotesis
Si llega a ser posible pero se debe poner uno  condicional  o dos condicionales con los dos botones }
#### Codigos


# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.GIRAFFE)
        sleep(400)
