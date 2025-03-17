``` js
from microbit import *
import utime
import music

class Bomba:
    def __init__(self):
        self.duracion = 20
        self.state = 'Configuracion'
        self.start_time = 0
        display.scroll(self.duracion)
        self.Codigo_Completado = False
        self.Total = 0

        self.clave1 = 0
        self.clave2 = 0
        self.clave3 = 0
        self.clave4 = 0 

        self.presionardenuevo = False
        self.presionardenuevo2 = False

    def update(self):
        
        display.scroll(self.duracion)

        if self.state == 'Configuracion':
            if button_a.was_pressed():
                if self.duracion < 61:
                    display.scroll(self.duracion)
                    self.duracion += 1 
                
            if button_b.was_pressed():
                if self.duracion > 9:
                    display.scroll(self.duracion)
                    self.duracion -= 1
                            

            
            if accelerometer.was_gesture('shake'):
                display.scroll('Armada')

                self.startTime = utime.ticks_ms()
                self.state = 'Armado'

        elif self.state == 'Armado':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > 1000:
                self.startTime = utime.ticks_ms()
                self.duracion -=1
                display.scroll(self.duracion)

                if button_a.was_pressed():
                    self.clave1 = 2
                    self.presionardenuevo = True
                    display.scroll('A')
                
                if button_b.was_pressed():
                    self.clave2 = 20
                    self.presionardenuevo2 = True
                    display.scroll('B')
                    
                if button_a.was_pressed() and self.presionardenuevo == True and self.presionardenuevo2 == True:
                    self.clave3 = 2
                    display.scroll('C')
                    
                if accelerometer.was_gesture('shake'):
                    self.clave4 = 10
                    self.Total = self.clave1+self.clave2-self.clave3/self.clave4
                    if self.Total == 21.8:
                        display.scroll('Desarmada')
                        self.duracion = 20
                        self.state = 'Configuracion'
                    else: 
                        self.clave1 = 0
                        self.clave2 = 0
                        self.clave3 = 0
                        self.clave4 = 0
                        display.scroll('M')
                
                if self.duracion == 0:
                    music.play(music.NYAN)
                    display.show(Image.SKULL)
                    self.state = 'Explosion'
            
        elif self.state == 'Explosion':
            if pin_logo.is_touched():
                self.duracion = 20
                display.scroll(self.duracion)
                self.state = 'Configuracion'

bomba = Bomba()

while True:
    bomba.update()
```
