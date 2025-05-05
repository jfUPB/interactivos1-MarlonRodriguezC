
Se utilizan como forma de pinceles para nuestras ilustraciones 

-hasta ahora nos daba el error ReferenceError: connectBtnClick is not defined pero ya  con esto se soluciona 


-si puedo verlo, si este no recibe datos , entonces el protagonista no devolverá nada y no se podría ejecutar el if (Data)


-Porque ocurre esto? porque el canva empieza en 0,0 en la parte superior izquierda de la pantalla, y este no es el centro de la pantalla, por tanto toca cortarlo, pero ahora solo quedaría en el centro superior de la pantalla, después de esto ,ya estaría centrado totalmente

-La forma mas simple para verificarlos tanto interna como externamente, es usando los condicionales con los booleanos y el print.
Los condicionales booleanos usan un método inverso a cada botón, me explico si el prevmicroBitAState es falso y el newAState es verdadero, entonces se cumple la condición para activar la tecla A, pero encambio si es prevmicroBitBState  es verdadero y el newBState es falso, se cumple la condición para activar la tecla B, y ambos realizan un print para demostrar que se logro el proceso

-el updateButtonStates verifica el actual estado del micro:bit, ósea puede dectectar si un botón pasa de estar presionado a no estarlo, y si no almacena el estado anterior pues esto no podría registrar un "cambio" dentro de los botones, entonces si seguiría ejecutando acciones que ya no se están haciendo  
