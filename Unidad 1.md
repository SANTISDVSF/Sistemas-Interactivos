## Unidad 1 - Trayecto de Actividades

### Ejercicio 6 - Sistemas Interactivos (Unidad 1)
#¿Cómo se ejecuta este programa?

R// 
Al comenzar, el programa se inicia en un estado llamado INIT, donde configura la comunicación serial para enviar datos y guarda el tiempo actual. Luego, pasa al estado WAIT_TIMEOUT, 
donde espera que pase un segundo. En cada ciclo del programa (gracias a la función loop()), se verifica si ha pasado ese segundo y, cuando ocurre, envía el tiempo actual al monitor 
serie y vuelve a empezar la espera. Este proceso se repite indefinidamente, enviando el tiempo cada segundo.

#- Pudiste ver este mensaje: Serial.print("Task1States::WAIT_TIMEOUT\n");. ¿Por qué crees que ocurre esto?
R//
Porque se imprime justo la primera vez que el programa entra en el estado WAIT_TIMEOUT. Esto sucede después de que se configura la comunicación y se guarda el tiempo actual. 
Así que, al cambiar de INIT a WAIT_TIMEOUT, el programa muestra ese mensaje en el monitor serie para indicar que está listo para empezar a contar el tiempo y enviar datos.

#- ¿Cuántas veces se ejecuta el código en el case Task1States::INIT?
R// Task1States::INIT se ejecuta solo una vez al inicio del programa. Esto sucede cuando el microcontrolador se arranca y llama a la función setup(), 
donde se configura todo por primera vez. Después de eso, el programa cambia al estado WAIT_TIMEOUT y nunca vuelve al estado INIT a menos que se reinicie.
