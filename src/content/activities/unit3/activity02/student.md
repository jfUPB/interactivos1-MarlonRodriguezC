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
        self.presionarparab = False
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
                    self.presionarparab = True
                    display.scroll('A')
                
                if button_b.was_pressed() and self.presionarparab == True:
                    self.clave2 = 20
                    self.presionardenuevo2 = True
                    display.scroll('B')
                    
                if button_a.was_pressed() and self.presionardenuevo == True and self.presionarparab == True and self.presionardenuevo2 == True:
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

Para implementar la secuencia de desactivacion primero pense en hacer un contador y con cada vez que se presionara un boton, si el contador llegaba a un numero especifico este desactivaria la bomba, pero me di cuenta que no estaria siguiendo cronologicamente la secuencia de la bomba y que podrias presionar el mismo boton y la maquina no lo notaria.

Luego pensar un rato y  usar una fila de IF, probar los booleanos y demas me di cuenta que al presionar un boton se podria guardar un numero el cual podria ser usar en una operacion matematica junto a los demas numeros (obviamente provenientes de otros botones), podria salir un numero especifico de esa operacion, no importaba si cambiaban de lugar los numeros, ya que podria dar un resultado distinto, por decirlo asi si juntamos 1+2+3 , y los intercambiamos, siempre nos va a dar 6, pero si hacemos 1x2/3 y los vamos interacambiando, nos damos cuenta que su patron es unico, entonces tome el patron de self.clave1+self.clave2-self.clave3/self.clave4 y si este era igual a 21.8, se desactivaria la bomba
