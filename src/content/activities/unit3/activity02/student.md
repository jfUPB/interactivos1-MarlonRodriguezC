from microbit import *
import utime
import music

class Bomba:
    def __init__(self):
        self.duracion = 20
        self.desactivar = 0
        self.state = 'Configuracion'
        self.start_time = 0
        display.scroll(self.duracion)
        self.Codigo_A = False
        self.Codigo_B = False
        self.Codigo_C = False
        self.Codigo_D = False 
 

    def update(self):

        if self.state == 'Configuracion':

            display.scroll(self.duracion)

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
                    self.desactivar += 1
                    self.Codigo_A = True
                    display.scroll('A')
                    
                if button_b.was_pressed():
                    self.desactivar += 1
                    self.Codigo_B = True
                    display.scroll('B')
                    
                if accelerometer.was_gesture('shake'):
                    self.desactivar += 1 
                    self.Codigo_C = True
                    
                if self.desactivar == 3:
                    display.scroll('Desarmada')
                    self.duracion = 20
                    self.state = 'Configuracion'
                    
                                
                        
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


    La secuencia se puso en el estado Armado, este por medio de IF 
