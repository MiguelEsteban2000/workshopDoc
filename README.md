# Workshop#7
Para el workshop de esta semana vamos a conectar dos microcontroladores por medio del protocolo I2C, para el cual es necesario que un microcontrolador actúe como esclavo y el otro como maestro, también para la comunicación se necesitan la conexión de dos cables. El objetivo de esto es que un microcontrolador que actúa como esclavo reciba la señal de un sensor de temperatura y este la envié al otro microcontrolador que actúa como maestro, para validar los datos y después prender un led si la temperatura supera 30 grados centígrados,para esto se necesita un Arduino y un senor como los de las siguentes imagenes  imagen.

<br>

![descarga](https://user-images.githubusercontent.com/53841624/168942233-fad2743d-dc59-4def-9158-6f2665eaa024.jpg)

<br>

![sensor](https://user-images.githubusercontent.com/53841624/168950105-a4029342-bc8c-43fb-9a19-c33b89610828.jpg)

La conexión de los dos Arduino se mostrará en la siguiente imagen.
![Smooth_Juttuli](https://user-images.githubusercontent.com/53841624/168949968-4e99a129-45d5-4f11-836f-92c5abb28456.jpg)

Vamos a explicar el código por la parte del maestro

Exportamos la librería wire para la comunicación y definimos el led que vamos a usar par indicarle al usuario cuando se pasaron los 30 grados.

<br>

![1m](https://user-images.githubusercontent.com/53841624/168950965-b024d595-ba4d-41d9-97d2-9e6217b8d94b.png)


<br>

En el setup iniciamos la consola para depurar, declaramos la variable del led como salida e inicializamos la librería wire para la comunicación.

![2m](https://user-images.githubusercontent.com/53841624/168950465-ed94bcc0-e5e3-4ea5-aa1e-8019fe9ee5e5.png)

En el loop iniciamos la trasmisión al dispositivo con la dirección 1, después se ponen la cola los bytes para la trasmisión y después terminamos la trasmisión y enviamos los datos que estaban en cola, después se piden los datos del esclavo, con la dirección y 1 byte, esto para pedirle al esclavo que cantidad de bytes tiene la información que va a enviar después, los lee para guárdalos en una variable y después pide todos estos bits con la cantidad de información que le va a enviar el esclavo, después de esto en un while vamos concatenando la información que nos llega del esclavo para tener el datos de la temperatura completo.
Después simplemente se convierten los datos a float para posteriormente comprobar si la temperatura excede los 30 grados, si lo hace, el led se prende y todo este proceso se hace cada segundo.

![3m](https://user-images.githubusercontent.com/53841624/168950919-8624751e-0165-4a61-878e-b919a4774e12.png)



Ahora vamos a explicar del esclavo.

En esta primera parte declaramos las variables que usaremos en la solución y exportamos la librería wire para la comunicación

![1e](https://user-images.githubusercontent.com/53841624/168950756-0e76d1f0-2645-457f-b6b5-631d71248586.png)


En el setup declaramos el uso de la consola para depurar el código, iniciamos la librería wire, declaramos que funciones se usaran cuando el esclavo reciba y pida datos.

<br>

![2e](https://user-images.githubusercontent.com/53841624/168950767-9cca3a33-fd44-4abe-a5d9-824344639205.png)

<br>

En el loop recibimos la temperatura del sensor, usamos una ecuación para tener la temperatura en grados centígrados, imprimimos por consola la temperatura y ejecutamos este proceso cada segundo.

<br>

![3e](https://user-images.githubusercontent.com/53841624/168950779-7af77dfc-2822-438b-9808-b5a774dbde76.png)

<br>

En la función receiveEvent se lee la información que envía el maestro y se comprueba si está solicitando que cantidad de datos se necesitan para la trasmisión

<br>

![4e](https://user-images.githubusercontent.com/53841624/168951157-82bec317-1bb4-4e45-9bfe-e29370569a0d.png)

<br>

En la función eventoSolicitud se comprueba si el maestro pidió la cantidad de datos a mandar o si pidió ya la información como tal, en ambos casos, envía la información solicitada por el maestro.

<br>

![5e](https://user-images.githubusercontent.com/53841624/168951174-de262211-7e78-4d44-aa62-220d0d61cc41.png)

<br>
