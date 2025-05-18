
### Explicación

El programa logra hacer varias cosas a la vez ya que al iniciar un estado, este toma las diferentes posibilidades que el usuario puede tomar al tocar el boton 'a' o espear que se se complete el intervalo de tiempo estipulado segun el estado (recordemos que cada estado tiene un intervalo de tiempo distinto) al tomar estas posibilidades hace uso de los condicionales para ejecutar la accion y esta hace que viaje a otro estado el cual repetira el proceso de esperar una orden por parte del boton o cumplir su intervalo de tiempo

Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.

1.vector: este vector inicia en 'STATE_HAPPY', donde al ser presionado el boton 'a' mostrara la imagen 'sad' y reiniciara el tiempo y empezara a usar el intervalo de 'SAD_INTERVAL' y empezara el estado de 'STATE_SAD', ya en el estado de 'STATE SAD' tendra que cumplir el tiempo de intervalo para mostrar la imagen 'happy', reiniciara el tiempo y volvera al estado 'STATE_HAPPY'

2.vector: este vector inicia en STATE_HAPPY, pero a diferencia del vector pasado aqui tendremos que esperar que se cumpla el tiempo de intervalo donde nos mostrara la imagen 'smile', se reiniciara el tiempo y empezara a usar el intervalo de 'SMILE_INTERVAL', aqui ya iniciara el estado 'STATE_SMILE' y si se presiona el boton 'a' este mostrara la imagen 'happy' reiniciara el tiempo y empezara a usar el intervalo de  'happy'

3.vector: este vector repite el proceso del vector 2 pero dentro del estado 'STATE_SMILE' no se presiona el boton 'a' , se debe esperar a que el tiempo sea mayor al intervalo (asi como paso del estado 'STATE_HAPPY' al 'STATE_SMILE') y nos mostrara la imagen de 'sad' y reiniciara el tiempo y tomara el intervalo de tiempo de 'SAD_INTERVAL' y cambiaremos al estado  'STATE_SAD' y aqui  tomaremos las mismas acciones del vector 1 de   'STATE_SAD' al cambiar a 'STATE_HAPPY'
 
