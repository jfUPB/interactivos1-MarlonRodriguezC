
Se utilizan como forma de pinceles para nuestras ilustraciones 

-hasta ahora nos daba el error ReferenceError: connectBtnClick is not defined pero ya  con esto se soluciona 


-si puedo verlo, si este no recibe datos , entonces el protagonista no devolverá nada y no se podría ejecutar el if (Data)


-Porque ocurre esto? porque el canva empieza en 0,0 en la parte superior izquierda de la pantalla, y este no es el centro de la pantalla, por tanto toca cortarlo, pero ahora solo quedaría en el centro superior de la pantalla, después de esto ,ya estaría centrado totalmente

-La forma mas simple para verificarlos tanto interna como externamente, es usando los condicionales con los booleanos y el print.
Los condicionales booleanos usan un método inverso a cada botón, me explico si el prevmicroBitAState es falso y el newAState es verdadero, entonces se cumple la condición para activar la tecla A, pero encambio si es prevmicroBitBState  es verdadero y el newBState es falso, se cumple la condición para activar la tecla B, y ambos realizan un print para demostrar que se logro el proceso

-el updateButtonStates verifica el actual estado del micro:bit, ósea puede dectectar si un botón pasa de estar presionado a no estarlo, y si no almacena el estado anterior pues esto no podría registrar un "cambio" dentro de los botones, entonces si seguiría ejecutando acciones que ya no se están haciendo  


Se ven algunas diferencias (por fuera de lo ya antes mostrado en la actividad) como por ejemplo antes para cambiar el color se usaba el espacio y ahora es B quien lo hace, ya en el código actual no, en el tema del screenshot el código anterior usaba un timestamp() para la especificación de su hora, día, mes, año, pero en el código actual este utiliza una linea de código individualmente de cada dato para guardarlos .
También el uso de los case "STATES.WAIT_MICROBIT_CONNECTION" y "STATES.RUNNING:" , para verificar si se puede dibujar segun si el micro:bit esta conectado y el segundo caso STATES.RUNNING: llegado el caso si el micro:bit no esta conectado y tambien  un if (microBitAState === true), el cual puede hacer funciones ya antes vista como la que vimos en el codigo anterior de poder "alinear" las ilustraciones si se presionaba shift

Cosas como la funcion connectBtnClick() ya son nuevas (y ya fueron descritas en el texto) pero esto va conectado con el en el setup() se hizieron un par de modificaciones como la creacion dle boton para conectar el micro:bit y la funcion windowResized(), la cual ya estaba dentro del codigo

De resto la funcion  updateButtonStates (usada para los botones A y B) es nueva y se le hizieron unas modificaciones a draw(), y esta es la que esta dando el print ("No se están recibiendo 4 datos del micro:bit") al no "llenar" los 4 valores esperados (posicion y boton A y B)
