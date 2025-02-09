Explorando el Micro:bit y Micropython
Enunciado: investiga las características del micro:bit y las funciones básicas de Micropython para controlarlo. Consulta en los recursos.

Recursos:

Características del micro:bit
Referencia
Entrega: en tu bitácora indica

Al menos 4 entradas y 4 salidas del micro:bit con su descripción.
Descripción de al menos 3 funciones de Micropython para entradas y 3 para salidas, con ejemplos de código sencillos.

#### Dispositivos de entrada

1. botones: los botones dentro del micro:bit son A y B cada uno esta repartido a un costado del microbit, y existe otro boton de reinicio
   
3. pines analogicos : su proposito es leer sensores externos como un potencianometro o un sensor de temperatura
4. microfono: logra reaccionar a  sonidos y poder medir los niveles de ruido
5. Acelometro: mide el movimiento del micro:bit si se rota o se mueve arriba o abajo

#### Dispositivos de salida

1.Altavoz : emite sonidos 

2.matriz de LEDS : muestran al usuario imagenes o texto en una cuadricula 5x5

3.Radio/Bluetooth: el micro:bit tambien permite a sus usuarios conectar los microbits entre si, logrando enviarse entre si sonidos o imagenes 

4.Led amarillo unico: funciona para informar cuando estas descargando un programa y se enciende para avisar que esta alimentado al conector USB

#### Ejemplos
Con el uso de la radio se pueden enviar dos personas caritas felices si se utiliza el siguiente codigo:


from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    if button_b.is_pressed():
        display.show("B")

