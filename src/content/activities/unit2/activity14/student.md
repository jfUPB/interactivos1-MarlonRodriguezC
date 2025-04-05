

#### 1. Vector configuracion del tiempo
Dentro del modo configuracion se toma la  variable de duracion (la cual sera de 20) y esta se podra editar subiendo o bajando sus cifras segun la 
decision del usuario con ayuda de los botones

#### 2. Vector  confirmacion del ajuste de tiempo dentro de la bomba
Al  hacer un shake al micro:bit este entrara en un modo donde confirma la cuenta regresiva de la bomba 
#### 3. Vector  cuenta regresiva
Durante la cuenta regresiva se restara el tiempo transcurrido al tiempo de duracion asignado y el tiempo real se mostrara la resta, mostrando como
poco a poco la cuenta regresiva llega a 0 y explota 
#### 4. Explosion
Al explotar esta emitira un sonido en especifico y una imagen de una calavera en los LEDs

#### 5. Reincio de la bomba?
Y si se toca el boton pin logo del micro:bit este volvera en su modo de configuracion


Los errores que note dentro de la creacion de mi bomba fueron corregidos por mi profesor, ya que por ejemplo olvide que el tiempo de cuenta regresiva
tenia cierto limite (no menor que 10, no mayor que 60) y olvide completamente esta orden, pero el mayor error fue encuanto optimizacion ya que usaba 
mucho el codigo " while True: " el cual aunque no parecia ocurrir mucho cuando activaba el codigo en el micro:bit, pero este codigo enverdad estaba haciendo que tuviese que pasar por muchos bucles y intentando repetir codigo inecesario y tomando mas recursos esperados , para esto lo cambio a un solo while true el cual tuviese un update y asi solamente un ciclo , adjunto codiog corregido:
```js
from microbit import *
import utime
import music

class Bomba:
    def __init__(self):
        self.duracion = 20
        self.state = 'Configuracion'
        self.start_time = 0
        display.scroll(self.duracion)

    def update(self):

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
