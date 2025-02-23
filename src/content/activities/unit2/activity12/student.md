``` js
from microbit import *
import utime
import music

class Bomba:
    def __init__(self):
        self.duracion = 20000  


    def configuracion(self):
        while True:  
            display.scroll(str(self.duracion // 1000))  
            
            if button_a.was_pressed():
                display.scroll('UP')
                self.duracion += 1000
            if button_b.was_pressed():
                display.scroll('DOWN')
                self.duracion -= 1000
            sleep(200)

            if accelerometer.was_gesture('shake'):
                self.Armado()
                
    def Armado(self):
        while True:
             for i in range(self.duracion // 1000, -1, -1):  # De duración a 0
                display.show(str(i))
                sleep(1000)
             self.Explosion()
    def Explosion(self):
        music.play(music.NYAN)
        while True:
            if pin_logo.is_touched():
                self.configuracion()
    
            
bomba = Bomba()
bomba.configuracion()
```
