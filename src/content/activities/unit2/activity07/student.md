#### Codigo
``` js
# Imports go at the top
from microbit import *
import music
import speech


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.was_pressed() or button_b.was_pressed():
        music.play(music.NYAN)
           
   
    
    if accelerometer.was_gesture('right'):
        display.show(Image.ARROW_E)
        audio.play(Sound.MYSTERIOUS)
```

#### Explicacion
Para activar los sonidos en la primera condicion IF se debe presionar el boton A o el boton B, OJO no confundir WAS presssed a Is pressed , uno es en pasado y el otro en presente, si se cumple la condicion de tocar
algunos de los dos botones dara la cancion NYAN.
Para la segunda condicion IF se usa el acelerometro y este reaccion siempre y cuando se gire el micro:bit a la derecha, este mostrara una imagen de una flecha señalando a la derecha y empezara a sonar algun 
sonido misterioso
