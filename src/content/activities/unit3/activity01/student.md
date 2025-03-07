from microbit import *
import utime

class Semaforo:
    def __init__(self, estado, tiempo_inicial, duracion_rojo, duracion_amarillo, duracion_verde, posicion):
        self.estado = estado
        self.tiempo_inicial = tiempo_inicial
        self.duracion_rojo = duracion_rojo
        self.duracion_amarillo = duracion_amarillo
        self.duracion_verde = duracion_verde
        self.posicion = posicion
    
    def mostrar_luz(self):
        # Apagar todas las luces antes de mostrar la actual
        display.clear()
        if self.estado == "Rojo":
            display.set_pixel(self.posicion[0], self.posicion[1], 9)  # Brillo máximo (rojo)
            
        elif self.estado == "Amarillo":
            display.set_pixel(self.posicion[0], self.posicion[1], 5)  # Brillo medio (amarillo)
            
        elif self.estado == "Verde":
            display.set_pixel(self.posicion[0], self.posicion[1], 2)  # Brillo bajo (verde)

    def cambiar_estado(self):
        tiempo_actual = utime.ticks_ms()
        

        if self.estado == "Rojo" and utime.ticks_diff(tiempo_actual, self.tiempo_inicial) > self.duracion_rojo:
            self.estado = "Amarillo"
            self.tiempo_inicial = tiempo_actual  
            
        elif self.estado == "Amarillo" and utime.ticks_diff(tiempo_actual, self.tiempo_inicial) > self.duracion_amarillo:
            self.estado = "Verde"
            self.tiempo_inicial = tiempo_actual  

        elif self.estado == "Verde" and utime.ticks_diff(tiempo_actual, self.tiempo_inicial) > self.duracion_verde:
            self.estado = "Rojo"
            self.tiempo_inicial = tiempo_actual  

    def update(self):
       
        self.cambiar_estado()
        self.mostrar_luz()

# Instanciar los semáforos con las luces y tiempos correspondientes
semaforo1 = Semaforo("Rojo", utime.ticks_ms(), 5000, 2000, 3000, (0, 0))
semaforo2 = Semaforo("Rojo", utime.ticks_ms(), 3000, 1000, 2000, (2, 0))
semaforo3 = Semaforo("Rojo", utime.ticks_ms(), 4000, 3000, 2000, (4, 0))

while True:
    # Actualizamos los semáforos llamando a su método 'update'
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
    


