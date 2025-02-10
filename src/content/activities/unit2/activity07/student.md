# Imports go at the top
from microbit import *
import music
import speech


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.was_pressed() or button_b.was_pressed():
        music.play(music.NYAN)
           
   
    
    if accelerometer.was_gesture('right'):
        display.show(Image.ARROW_E)
        audio.play(Sound.MYSTERIOUS)
