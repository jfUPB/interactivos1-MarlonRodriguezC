
#### Que quiero comprobar?
Es posible hacer una accion con la condicion de presionar A y B al mismo tiempo?
#### Hipotesis
Si llega a ser posible pero se debe poner uno  condicional  o dos condicionales con los dos botones }
#### Codigos

``` js
# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.GIRAFFE)
        sleep(400)
```

#### Descripción de lo resultados
Se utiliza el comando "and"  dentro de la condicion IF donde se señala que si es precionado el boton A y el boton B
al cumplir esta condicion se muestra la imagen girafa

#### Análisis de esos resultados
Por lo visto se puede usar solo una condicion IF dentro del codigo para lograr esto, algo similar a lo que seria && en C# donde los devuelve un true siempre y cuando los dos operandos son true

#### Conclusiones
Es posible ejecutar una accion cuando los botones A y B son presionados al mismo tiempo con solo una condicion IF utilizando el comando "and"
