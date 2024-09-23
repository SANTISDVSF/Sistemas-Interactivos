## Unidad 2. Protocolos ASCII

¿Quién debe comenzar primero la comunicación, el computador o el controlador? ¿Por qué?
En este caso, el controlador (Raspberry Pi Pico) debe comenzar primero la comunicación. Esto se debe a que el controlador necesita estar preparado para recibir datos antes de que el computador envíe cualquier señal. Al iniciar primero el controlador con Serial.begin(), se establece una conexión en el puerto serial, lo que permite que el computador envíe datos una vez que esté listo.

¿Cómo funciona la aplicación con ScriptCommunicator?
La aplicación con ScriptCommunicator permite establecer una conexión entre el computador y el controlador, facilitando la comunicación serial. Al enviar el carácter '1' desde el computador, el controlador responde con "Hello from Raspberry Pi Pico". Esta comunicación es fundamental para probar que ambos dispositivos están correctamente conectados y pueden intercambiar datos.

¿Por qué es importante considerar las propiedades PortName y BaudRate?
Es importante considerar las propiedades PortName y BaudRate porque PortName asegura que el computador se conecte al puerto correcto donde está el controlador, mientras que BaudRate determina la velocidad a la que se envían y reciben los datos. Si estas configuraciones no son correctas, la comunicación entre ambos dispositivos fallará, lo que podría impedir que funcionen juntos de manera efectiva.

