from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.estado = "Rojo"
        self.tiempo_inicial = utime.ticks_ms()
        self.duracion_rojo = 5000  
        self.duracion_amarillo = 5000  
        self.duracion_verde = 5000  
        self.luces = {  
            "Rojo": (0, 0),
            "Amarillo": (0, 1),
            "Verde": (0, 2),
        }


    def mostrar_luz(self):
        if self.estado == "Rojo":
            display.set_pixel(0, 0, 9)  
            
        elif self.estado == "Amarillo":
            display.set_pixel(0, 1, 9)
            
        elif self.estado == "Verde":
            display.set_pixel(0, 2, 9)  

    def cambiar_estado(self):
        if self.estado == "Rojo" and utime.ticks_diff(utime.ticks_ms(), self.tiempo_inicial) > self.duracion_rojo:
            self.apagar_luz(self.estado) 
            self.estado = "Amarillo"
            self.tiempo_inicial = utime.ticks_ms()  # Reiniciar el tiempo
            
        elif self.estado == "Amarillo" and utime.ticks_diff(utime.ticks_ms(), self.tiempo_inicial) > self.duracion_verde:
            self.apagar_luz(self.estado) 
            self.estado = "Verde"
            self.tiempo_inicial = utime.ticks_ms()
        elif self.estado == "Verde" and utime.ticks_diff(utime.ticks_ms(), self.tiempo_inicial) > self.duracion_amarillo:
            self.apagar_luz(self.estado)
            self.estado = "Rojo"
            self.tiempo_inicial = utime.ticks_ms()

    def apagar_luz(self, estado):
        x, y = self.luces[estado]
        display.set_pixel(x, y, 0)
        
semaforo = Semaforo()

while True:
    semaforo.mostrar_luz()
    semaforo.cambiar_estado()
