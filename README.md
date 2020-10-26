# AR-LYNUX

English Tutorial for Beginners
Local lenguage: Spanish

- Walkthrough Video: https://youtu.be/ndfmYPulFF4
- Full Video Tutorial: https://youtu.be/dQkNVcW_oG0
- Download Spark AR Software: https://sparkar.facebook.com/ar-studio/download/

## ENGLISH TUTORIAL
In this tutorial we are going to make an ARGame for Instagram using Spark AR. 

The game will consist on having 3D letters floating all around us, one letter will appear, and we will have to look for it in a 360 world space. Once we find the correct one we tap on it and confetti and sound will come up.

###### FIRST STEP: BRING THE OBJECTS

First we will add the letters to the scene, we need two null objects, one will contain the letters that will float, and the other one the letters that will show up and let us know which one we will have to find. You can make one then duplicate it.

Add asset, null object then add 3d text, then write the letter. Once we have both null objects with the letters, we will reubicate the floating letters on the scene, we need them to be out of the camera view, so just separate them and put them around the camera point and the camera view. 

We want them to be seen just with the back camera so, we drag the Camera to the patch editor, we connect the back camera to a Delay because we want the floating letters to appear few seconds before the letter we have to find, we connects it’s null object to the delay. For the beginning letters we will also connect its null object to the Delay but in this case we are going to put a Not between them, so the delay won’t affect. 

###### SECOND STEP: CONNECTING THE LETTERS

To the back camera we connect a pulse and a random patch, from 1 to 4 because we have 4 letters (it could also be from 0 to 3), we add a round patch the link it to equals exactly, the second numbers from that patch has to increase with each letter, A would be 0 or 1, B would be 1 or 2. From equals exactly we have two paths, one is the letter that will show up at the beginning, we directly connect to the visibility property of the letter. The other path is the information sent, which object has shown and which one has to react when we touch it. We drag the floating letter to the patch editor, now we have to link the letter patch and the equals exactly to an object tap. What we want is that once we tap on the correct letter something appears and let us know that was the correct one.

###### THIRD STEP: ADDING TRANSITION, SOUND AND PARTICLES

SOUND.

Add asset, from AR Library, we import the sound we prefer, we drag it to the patch editor. To object tap we add, SINGLE CLIP CONTROLER then an AUDIO PLAYER, we link the sound to the audio player audio clip, and then to its speaker.  

PARTICLES CONFETTI.

ADD OBJECT then PARTICLE SYSTEM, modify it so it looks like confetti or whatever you want. Object tap, then switch the delay because we don’t want it to appear right away, delay of 1 second, then add the visibility of the emitter.

 
CHANGING SCALE OR ROTATING

OBJECT TAP, SWITCH, LOOP ANIMATION, TRANSITION then the letter scale patch. We want it to increase once we tap it, so we have to set the start values to 3 (this will be the start scale of the letter) then the end value to 8 or so ,  and make it linear. We can also make it rotate, we just need to bring its rotation patch. 


###### FORTH STEP: ROTATING THE LETTERS AROUND US

Once we have all, we want the letters to float around us so it makes the game kind of tricky, we have to open the patch editor, and click the 3d rotation of the null object. 
We add the following patches: Loop animation and transition and we link them to the 3d rotation
We set the duration to 20 and the end transition of the y axis to 360. 
If you also want to 3d rotate the letter on their selves you have to do the same steps but with their 3d rotation, this time the duration could be set to 8 so they move a bit faster.

LETTERS ROTATING ON THEIR AXES
We do the same as we did with the floating letters but in this case we take the rotation from each letter, and set the end Y axis to 360.

###### FIFTH STEP: INSTRUCTION

We want the users to know that the filter only works on the back camera, so we go to Device add instructions and set the Flip Camera instruction it will automatically give us the patch, I recomendó to change the time from 5 to 3.

IF WE WANT MORE LETTERS WE JUST NEED TO REPLICATE EXACTLY WHAT WE HAVE DONE. 


###### ADVANCED START

In this case, we will have a play icon nothing else appearing on the screen, once we are ready we touch start and a letter will show up, that’s the one we have to find, after that a countdown will start and once it finishes the floating letters will appear.

We have to add a plane, and on that plane a start icon. 

We drag the plane to the patch editor, what we want is that once we tap on the start a random letter shows up and it automatically sends the info of which letter has shown. 

We connect an Object tap to the plane, then to the  increase part of the counter, the maximum count would be 2, we connect that to the option part of an OPTION SENDER, on the output 0 we are going to link the letters that you have to find, and on the output 1 the letters that will float around us, we want them to appear few seconds before the letter that we have to find so,  from output 1 we have to connect a NOT signal and a DELAY, we set the delay to 4 seconds, and then we have to click on the visible arrow of the rotating letters.

Now lets go to the random letter. 
We are on the OPTION SENDER Output 0, we connect a pulse and a random patch, from 1 to 5 cause we have 4 letters, we add ROUND patch then EQUALS EXACTLY from equal exactly we have to paths, one is the letter that will show up at the beginning, we directly connect to the visibility property. The other path is the information we have to send, which object has shown and which one has to react when we touch it. We drag the floating letters to the patch editor, now we have to link the letter patch and the equals exactly patch to an OBJECT TAP, now we want is that once we tap on the correct letter something appears and let us now that was the correct one. (FOLLOW THE SAME STEPS WE DID BEFORE)


###### SEARCH THIS OBJECT INSTRUCTION (not allowed on Instagram or facebook)
We have a start icon and “Search this object” we select it and make it a texture sequence.  Add asset and add an animation sequence, then add de texture sequence. 

To the option sender output 0 we link a PULSE and then to the play Animation, on the animation sequence we select CURRENT FRAME and connect it to the progress from the animation. 

This means we will have the play and once we touch it the instructions will pop out.

###### COUNTDOWN TIMER (this could be also not allowed because of static text)

Add asset, add script, we write the code, then we charge it on spark. Script in TO SCRIPS we tap on plus and Add, Timer which has to be a number. We create a text named TimerText.

To the object tap we add a delay of 1 second, then we add this patch https://youtu.be/g2a93PBYEJ0 and to the patch we link the script Timer to the Time output, and to the Done output we add NOT and the TimerText. We want it to go from 3 to 0, and 1 second of speed.

// How to load in modules
const Scene = require('Scene');

// Use export keyword to make a symbol available in scripting debug console
export const Diagnostics = require('Diagnostics');

const Patches = require('Patches');


Promise.all([

    Scene.root.findFirst('TimerText'),

]).then(function (results) {

    const timerCountText = results[0];

    Patches.outputs.getScalar('Timer').then(timerObj => {

        timerObj.monitor().subscribe(function (timerEvent) {

            timerCountText.text = timerEvent.newValue.toFixed(2).toString();

        });

    });


});

## LOCAL LENGUAGE ESPAÑOL ( SPANISH ) TUTORIAL

En este tutorial vamos a hacer un juego AR para Instagram usando Spark AR.

El juego consistirá en tener letras 3D flotando a nuestro alrededor, aparecerá una letra y tendremos que buscarla en un espacio 360. Una vez que encontremos el correcto, lo pulsamos y aparecerán confeti y sonido.

###### PRIMER PASO: CREAR LOS OBJETOS

Primero agregaremos las letras a la escena, necesitamos dos objetos nulos, uno contendrá las letras que flotarán, y el otro las letras que aparecerán y nos dejarán saber cuál tendremos que encontrar. Puedes hacer uno y luego duplicarlo.

Agregue asset, objeto nulo, luego agregue texto en 3D, despúes escriba la letra. Una vez que tengamos ambos objetos nulos con las letras, reubicaremos las letras flotantes en la escena, necesitamos que estén fuera de la vista de la cámara, así que simplemente sepárelas y colóquelas alrededor del punto de la cámara y la vista de la cámara.

Queremos que se vean solo con la cámara trasera así que arrastramos la Cámara al editor de parches, conectamos la cámara trasera a un Delay porque queremos que las letras flotantes aparezcan unos segundos antes de la letra que tenemos que encontrar, conectamos es un objeto nulo para el retraso. Para las letras iniciales también conectaremos su objeto nulo al Delay pero en este caso vamos a poner un Not entre ellas, para que el delay no afecte.

###### SEGUNDO PASO: CONECTAR LAS LETRAS

A la cámara trasera conectamos pulse y  random, del 1 al 4 porque tenemos 4 letras (también podría ser del 0 al 3), agregamos un parche round que enlazamos con equals exaclty, los segundos números de ese. El parche tiene que aumentar con cada letra, A sería 0 o 1, B sería 1 o 2. De igual a exactamente tenemos dos caminos, uno es la letra que aparecerá al principio, conectamos directamente a la propiedad de visibilidad de la carta. El otro camino es la información enviada, qué objeto ha mostrado y cuál tiene que reaccionar cuando lo tocamos. Arrastramos la letra flotante al editor de parches, ahora tenemos que vincular el parche equals exactly a uno de object tap. Lo que queremos es que una vez que hagamos tapping en la letra correcta, aparezca algo y nos haga saber que era la correcta.

###### TERCER PASO: AÑADIR TRANSICIÓN, SONIDO Y PARTÍCULAS

SONIDO.

Agregar activo, desde AR Library, importamos el sonido que preferimos, lo arrastramos al editor de parches. Para tocar el objeto agregamos, SINGLE CLIP CONTROLERP y luego un AUDIO PLAYER, vinculamos el sonido al clip de audio del reproductor de audio y luego a su altavoz.

CONFETTI DE PARTÍCULAS.

AÑADIR UN OBJETO y luego  un SISTEMA DE PARTÍCULAS, modificarlo para que parezca confeti o lo que quieras. Toque el objeto, luego cambie el delay porque no queremos que aparezca de inmediato, retraso de 1 segundo, luego agregue la visibilidad del emisor.


CAMBIAR ESCALA O GIRAR

OBJETO TAP, SWITCH, LOOP ANIMATION, TRANSITION y luego el parche de escala de letras. Queremos que aumente una vez que lo toquemos, por lo que tenemos que establecer los valores de inicio en 3 (esta será la escala de inicio de la letra), luego el valor final en 8 más o menos, y hacerlo lineal. También podemos hacer que gire, solo necesitamos traer su parche de rotación.


###### CUARTO PASO: GIRANDO LAS LETRAS A nuestro alrededor

Una vez que tengamos todo, queremos que las letras floten a nuestro alrededor, por lo que hace que el juego sea un poco complicado, tenemos que abrir el editor de parches y hacer clic en la rotación 3D del objeto nulo.
Agregamos los siguientes parches: loop animation y transition y los vinculamos a la rotación 3d
Establecemos la duración en 20 y la transición final del eje y en 360.
Si también quieres rotar la letra en 3D, tienes que hacer los mismos pasos pero con su rotación en 3D, esta vez la duración podría establecerse en 8 para que se muevan un poco más rápido.

LETRAS GIRANDO SOBRE SUS EJES
Hacemos lo mismo que hicimos con las letras flotantes, pero en este caso tomamos la rotación de cada letra y establecemos el eje Y final en 360.

###### QUINTO PASO: INSTRUCCIÓN

Queremos que los usuarios sepan que el filtro solo funciona en la cámara trasera, así que vamos a Device add instructions y configuramos la instrucción gira la cámara que automáticamente nos dará el parche, recomiendo cambiar el tiempo de 5 a 3.

SI QUEREMOS MÁS LETRAS, SOLO NECESITAMOS REPLICAR EXACTAMENTE LO QUE HEMOS HECHO.

###### INICIO AVANZADO

En este caso tendremos un ícono de play nada más apareciendo en la pantalla, una vez estemos listos tocamos iniciar y aparecerá una letra, esa es la que tenemos que encontrar, luego de eso comenzará una cuenta atrás y una vez finalice la aparecerán letras flotantes.

Tenemos que agregar un plano y en ese plano un icono de inicio.

Arrastramos el plano al editor de parches, lo que queremos es que una vez que toquemos el inicio aparezca una letra aleatoria y automáticamente envíe la información de qué letra se ha mostrado.

Conectamos un tap de Objeto al plano, luego a la parte de aumento del contador, el conteo máximo sería 2, lo conectamos a la parte de opción de un OPTION SENDER, en la salida 0 vamos a vincular las letras que usted tenemos que encontrar, y en la salida 1 las letras que flotarán a nuestro alrededor, queremos que aparezcan unos segundos antes de la letra que tenemos que encontrar así que desde la salida 1 tenemos que conectar una señal NOT y un DELAY, ponemos el retraso a 4 segundos, y luego tenemos que hacer clic en la flecha visible de las letras giratorias.

Ahora vayamos a la letra aleatoria.
Estamos en la OPTION SENDER Outpout 0, conectamos pulse y un parche aleatorio, de 1 a 5 porque tenemos 4 letras, agregamos el parche ROUND y luego EQUALS EXACTLY  de igual exactamente tenemos a las rutas, una es la letra que mostrará al principio, nos conectamos directamente a la propiedad de visibilidad. El otro camino es la información que tenemos que enviar, qué objeto ha mostrado y cuál tiene que reaccionar cuando lo tocamos. Arrastramos las letras flotantes al editor de parches, ahora tenemos que vincular el parche de letras y el parche igual exactamente a un OBJETO TAP, ahora lo que queremos es que una vez que toquemos en la letra correcta aparezca algo y nos dejen ahora que era el correcto uno. (SIGA LOS MISMOS PASOS QUE HICIMOS ANTES)


###### BUSCAR ESTE OBJETO INSTRUCCIÓN (no permitido en Instagram o Facebook)
Tenemos un icono de inicio y “search this object” lo seleccionamos y lo convertimos en una secuencia de textura. Agregue activos y agregue una secuencia de animación, luego agregue la secuencia de textura.

A la opción remitente salida 0 enlazamos un PULSO y luego a la animación de reproducción, en la secuencia de animación seleccionamos FOTO ACTUAL y lo conectamos al progreso de la animación.

Esto significa que tendremos el juego y una vez que lo toquemos aparecerán las instrucciones.

###### COUNTDOWN TIMER (esto también podría no estar permitido debido al texto estático)

Agregue asset, agregue script, escribimos el código, luego lo cargamos en Spark. En el script TO SCRIPS, tocamos más y Add, Timer, que tiene que ser un número. Creamos un texto llamado TimerText.

Al toque del objeto agregamos un retraso de 1 segundo, luego agregamos este parche https://youtu.be/g2a93PBYEJ0 y al parche vinculamos el script Timer a la salida Time, y a la salida Done agregamos NOT y el TimerText. Queremos que pase de 3 a 0, y 1 segundo de velocidad.


// How to load in modules
const Scene = require('Scene');

// Use export keyword to make a symbol available in scripting debug console
export const Diagnostics = require('Diagnostics');

const Patches = require('Patches');


Promise.all([

    Scene.root.findFirst('TimerText'),

]).then(function (results) {

    const timerCountText = results[0];

    Patches.outputs.getScalar('Timer').then(timerObj => {

        timerObj.monitor().subscribe(function (timerEvent) {

            timerCountText.text = timerEvent.newValue.toFixed(2).toString();

        });

    });


});
