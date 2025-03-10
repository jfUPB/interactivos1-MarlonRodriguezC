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
        self.tiempo_inicial = utime.ticks_ms()
        while True:
            tiempo_transcurrido = utime.ticks_diff(utime.ticks_ms(), self.tiempo_inicial)
            tiempo_restante = (self.duracion - tiempo_transcurrido) // 1000

            if tiempo_restante >= 0:
                display.show(str(tiempo_restante))
            else:
                self.Explosion()

    def Explosion(self):
        music.play(music.NYAN)
        display.show(Image.SKULL)

        while True:
            if pin_logo.is_touched():
                self.configuracion()

bomba = Bomba()
bomba.configuracion()

```
https://youtube.com/shorts/07yUSXQr2JM
