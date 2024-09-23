## Unidad 1 - Trayecto de Actividades

### Ejercicio 6 - Sistemas Interactivos (Unidad 1)
¿Cómo se ejecuta este programa?

R// 
Al comenzar, el programa se inicia en un estado llamado INIT, donde configura la comunicación serial para enviar datos y guarda el tiempo actual. Luego, pasa al estado WAIT_TIMEOUT, 
donde espera que pase un segundo. En cada ciclo del programa (gracias a la función loop()), se verifica si ha pasado ese segundo y, cuando ocurre, envía el tiempo actual al monitor 
serie y vuelve a empezar la espera. Este proceso se repite indefinidamente, enviando el tiempo cada segundo.

Pudiste ver este mensaje: Serial.print("Task1States::WAIT_TIMEOUT\n");. ¿Por qué crees que ocurre esto?
R//
Porque se imprime justo la primera vez que el programa entra en el estado WAIT_TIMEOUT. Esto sucede después de que se configura la comunicación y se guarda el tiempo actual. 
Así que, al cambiar de INIT a WAIT_TIMEOUT, el programa muestra ese mensaje en el monitor serie para indicar que está listo para empezar a contar el tiempo y enviar datos.

¿Cuántas veces se ejecuta el código en el case Task1States::INIT?
R// Task1States::INIT se ejecuta solo una vez al inicio del programa. Esto sucede cuando el microcontrolador se arranca y llama a la función setup(), 
donde se configura todo por primera vez. Después de eso, el programa cambia al estado WAIT_TIMEOUT y nunca vuelve al estado INIT a menos que se reinicie.

### Ejercicio 7: análisis del programa de prueba

Observa la función 

```cpp
millis(); 
```

¿Para qué sirve?
R// Sirve para obtener el tiempo transcurrido desde que se inició el programa en milisegundos

### Ejercicio 8: retrieval practice (evaluación formativa)

¿Cuáles son los estados del programa?

INIT: Estado inicial donde se configura la comunicación serial y se establece el tiempo inicial.
WAITING: Estado donde el programa espera que transcurra el tiempo.
ONE_SECOND: Estado que se activa al pasar un segundo.
TWO_SECONDS: Estado que se activa al pasar dos segundos.
THREE_SECONDS: Estado que se activa al pasar tres segundos.

¿Cuáles son los eventos?

Transcurre 1 segundo: Ocurre cuando el tiempo acumulado alcanza 1000 milisegundos.
Transcurre 2 segundos: Ocurre cuando el tiempo acumulado alcanza 2000 milisegundos.
Transcurre 3 segundos: Ocurre cuando el tiempo acumulado alcanza 3000 milisegundos.

¿Cuáles son las acciones?

Enviar un mensaje de 1 segundo: Imprimir "1 segundo ha pasado" en el monitor serie.
Enviar un mensaje de 2 segundos: Imprimir "2 segundos han pasado" en el monitor serie.
Enviar un mensaje de 3 segundos: Imprimir "3 segundos han pasado" en el monitor serie.

### Ejercicio 12: punteros

¿Cómo se declara un puntero?
Un puntero se declara especificando el tipo de dato que va a apuntar, seguido de un asterisco (*)

¿Cómo se define un puntero? (cómo se inicializa)
Para definir un puntero, necesitas asignarle la dirección de una variable existente. Esto se hace usando el operador de dirección (&).

¿Cómo se obtiene la dirección de una variable?
La dirección de una variable se obtiene usando el operador de dirección (&)

¿Cómo se puede leer el contenido de una variable por medio de un puntero?
Para leer el contenido de una variable usando un puntero, se utiliza el operador de desreferencia (*). Esto permite acceder al valor de la variable a la que el puntero está apuntando

¿Cómo se puede escribir el contenido de una variable por medio de un puntero?
Para escribir el contenido de una variable a través de un puntero, también se utiliza el operador de desreferencia (*). Esto permite modificar el valor de la variable a la que el puntero apunta.

### Ejercicio 15: punteros y arreglos

1. ¿Por qué es necesario declarar rxData static? Y si no es static, ¿qué pasa?
rxData es static para que pueda recordar lo que guarda entre cada vez que el programa revisa los datos. Si no fuera static, se borraría cada vez que el programa volviera a esa parte, 
y no podrías acumular los datos que recibes.

2. dataCounter se define como static y empieza en 0. ¿Se reinicia a 0 cada vez que se entra al loop? ¿Por qué se declara como static?
dataCounter también es static, así que guarda su valor cada vez que revisas el programa. No se reinicia a 0. Esto es útil porque necesitas contar cuántos datos has recibido,
y quieres que siga contando hasta que llegues a 5.

3. El nombre del arreglo rxData se refiere a la dirección del primer elemento del arreglo. ¿Qué significa esto?
Esto quiere decir que cuando usas rxData sin los corchetes, estás hablando de la dirección donde comienza el arreglo. Es como tener la dirección de tu casa; si quieres ir a tu casa, solo necesitas esa dirección.

4. En la expresión sum = sum + (pData[i] - 0x30);, ¿cómo se usa el puntero pData para acceder a cada elemento del arreglo?
El puntero pData te permite acceder a los elementos del arreglo como si fuera una lista. Cuando usas pData[i], estás obteniendo el elemento que está en la posición i, lo que hace que sea fácil trabajar con los datos.

5.La constante 0x30 en (pData[i] - 0x30), ¿por qué es necesaria?
0x30 es el código que representa el carácter '0' en el sistema de codificación ASCII. Al restar 0x30 de un carácter como '3', lo conviertes en el número 3. Esto es importante porque quieres sumar los dígitos como números, no como letras.

### Ejercicio 16: análisis del api serial (investigación: hipótesis-pruebas)

¿Qué pasa cuando hago un Serial.available()?
Cuando se usa Serial.available(), se esta preguntando cuántos datos hay esperando en la cola para ser leídos. Si hay datos, te dice cuántos; si no, te dice que no hay nada.

¿Qué pasa cuando hago un Serial.read()?

Al llamar a Serial.read(), el programa lee el primer dato que llegó y lo saca de la cola. Este dato puede ser un número o un carácter, dependiendo de lo que enviaste.

¿Qué pasa cuando hago un Serial.read() y no hay nada en el buffer de recepción?
Si intentas leer con Serial.read() y no hay datos, el programa te devuelve -1. Eso significa que no hay nada para leer en ese momento.
Patrón común:

4. cpp
Copiar código
if (Serial.available() > 0) {
    int dataRx = Serial.read();
}
Este patrón es útil porque primero verificas si hay datos disponibles. Solo si hay algo en la cola, entonces lees el dato. Así evitas errores.

5. ¿Cuántos datos lee Serial.read()?
Serial.read() solo puede leer un solo dato a la vez. Si necesitas leer más de uno, tendrás que llamar a Serial.read() varias veces.

6. ¿Y si quiero leer más de un dato?
Si quieres leer varios datos, puedes usar un bucle que llame a Serial.read() tantas veces como necesites, siempre asegurándote de que haya datos disponibles antes de cada llamada.

7. ¿Qué pasa si te envían datos por serial y se te olvida llamar Serial.read()?
Si olvidas leer los datos, estos se quedarán en la cola. Si recibes muchos datos y el espacio se llena, los más viejos se perderán. Por eso, es importante leer los datos tan pronto como lleguen.

### Ejercicio 18: retrieval practice (evaluación formativa)





