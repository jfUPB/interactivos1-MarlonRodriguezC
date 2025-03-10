### Codigo
``` js
# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.PACMAN)
        sleep(400)
    

    if pin_logo.is_touched():
        display.show(Image.HAPPY)

    
    
    if accelerometer.was_gesture('face down'):
        display.show(Image.ASLEEP)
        display.scroll('score')    
        display.scroll(64)
```
#### Explicacion
El codigo funciona con 3 condicionales IF, el primero siempre y cuando se este presionando los botones A y B al mismo tiempo este mostrara un pacman, el segundo es activado si el logo del microbit (se encuentra encima de la 
matriz 5x5 de los LED) es tocado, mostrandonos una carita feliz,  y el tercero utiliza el acelerometro y se debe voltear el microbit boca abajo para mostrar la plabara "score" y despues mostrara el numero "64"
