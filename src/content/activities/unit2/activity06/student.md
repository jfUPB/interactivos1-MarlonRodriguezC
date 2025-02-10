# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.PACMAN)
        sleep(400)
    

    if pin_logo.is_touched():
        display.show(Image.HAPPY)

    
    
    if accelerometer.was_gesture('face down'):
        display.show(Image.ASLEEP)
        display.scroll('score')    
        display.scroll(64)
