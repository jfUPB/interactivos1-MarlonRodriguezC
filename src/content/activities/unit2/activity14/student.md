

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
mucho el codigo " while True: " el cual aunque no parecia ocurrir mucho cuando activaba el codigo en el micro:bit, este codigo enverdad estaba haciendo
que tuviese que guardar y estar al pendiente de mas informacion de la esperada y, para esto lo cambio a un solo while true el cual tuviese un update y 
este (al igual que los proyectos en unity) estuviese calculando  solamente un ciclo , aunque puse el codigo corregido debajo del mio en la actividad 12
igualmente adjuntare el codigo corregido aqui: 
