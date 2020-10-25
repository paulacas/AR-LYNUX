# AR-LYNUX
In this tutorial we are going to make an ARGame for Instagram using Spark AR. 

The game will consist on having 3D letters floating all around us, one letter will appear, and we will have to look for it in a 360 world space. Once we find the correct one we tap on it and confetti and sound will come up.

FIRST STEP: BRING THE OBJECTS

First we will add the letters to the scene, we need two null objects, one will contain the letters that will float, and the other one the letters that will show up and let us know which one we will have to find. You can make one then duplicate it.

Add asset, null object then add 3d text, then write the letter. Once we have both null objects with the letters, we will reubicate the floating letters on the scene, we need them to be out of the camera view, so just separate them and put them around the camera point and the camera view. 

We want them to be seen just with the back camera so, we drag the Camera to the patch editor, we connect the back camera to a Delay because we want the floating letters to appear few seconds before the letter we have to find, we connects it’s null object to the delay. For the beginning letters we will also connect its null object to the Delay but in this case we are going to put a Not between them, so the delay won’t affect. 

SECOND STEP: CONNECTING THE LETTERS

To the back camera we connect a pulse and a random patch, from 1 to 4 because we have 4 letters (it could also be from 0 to 3), we add a round patch the link it to equals exactly, the second numbers from that patch has to increase with each letter, A would be 0 or 1, B would be 1 or 2. From equals exactly we have two paths, one is the letter that will show up at the beginning, we directly connect to the visibility property of the letter. The other path is the information sent, which object has shown and which one has to react when we touch it. We drag the floating letter to the patch editor, now we have to link the letter patch and the equals exactly to an object tap. What we want is that once we tap on the correct letter something appears and let us know that was the correct one.

THIRD STEP: ADDING TRANSITION, SOUND AND PARTICLES

SOUND.

Add asset, from AR Library, we import the sound we prefer, we drag it to the patch editor. To object tap we add, SINGLE CLIP CONTROLER then an AUDIO PLAYER, we link the sound to the audio player audio clip, and then to its speaker.  

PARTICLES CONFETTI.

ADD OBJECT then PARTICLE SYSTEM, modify it so it looks like confetti or whatever you want. Object tap, then switch the delay because we don’t want it to appear right away, delay of 1 second, then add the visibility of the emitter.

 
CHANGING SCALE OR ROTATING

OBJECT TAP, SWITCH, LOOP ANIMATION, TRANSITION then the letter scale patch. We want it to increase once we tap it, so we have to set the start values to 3 (this will be the start scale of the letter) then the end value to 8 or so ,  and make it linear. We can also make it rotate, we just need to bring its rotation patch. 


FORTH STEP: ROTATING THE LETTERS AROUND US

Once we have all, we want the letters to float around us so it makes the game kind of tricky, we have to open the patch editor, and click the 3d rotation of the null object. 
We add the following patches: Loop animation and transition and we link them to the 3d rotation
We set the duration to 20 and the end transition of the y axis to 360. 
If you also want to 3d rotate the letter on their selves you have to do the same steps but with their 3d rotation, this time the duration could be set to 8 so they move a bit faster.

LETTERS ROTATING ON THEIR AXES
We do the same as we did with the floating letters but in this case we take the rotation from each letter, and set the end Y axis to 360.

FIFTH STEP: INSTRUCTION

We want the users to know that the filter only works on the back camera, so we go to Device add instructions and set the Flip Camera instruction it will automatically give us the patch, I recomendó to change the time from 5 to 3.

IF WE WANT MORE LETTERS WE JUST NEED TO REPLICATE EXACTLY WHAT WE HAVE DONE. 


ADVANCED START

In this case, we will have a play icon nothing else appearing on the screen, once we are ready we touch start and a letter will show up, that’s the one we have to find, after that a countdown will start and once it finishes the floating letters will appear.

We have to add a plane, and on that plane a start icon. 

We drag the plane to the patch editor, what we want is that once we tap on the start a random letter shows up and it automatically sends the info of which letter has shown. 

We connect an Object tap to the plane, then to the  increase part of the counter, the maximum count would be 2, we connect that to the option part of an OPTION SENDER, on the output 0 we are going to link the letters that you have to find, and on the output 1 the letters that will float around us, we want them to appear few seconds before the letter that we have to find so,  from output 1 we have to connect a NOT signal and a DELAY, we set the delay to 4 seconds, and then we have to click on the visible arrow of the rotating letters.

Now lets go to the random letter. 
We are on the OPTION SENDER Output 0, we connect a pulse and a random patch, from 1 to 5 cause we have 4 letters, we add ROUND patch then EQUALS EXACTLY from equal exactly we have to paths, one is the letter that will show up at the beginning, we directly connect to the visibility property. The other path is the information we have to send, which object has shown and which one has to react when we touch it. We drag the floating letters to the patch editor, now we have to link the letter patch and the equals exactly patch to an OBJECT TAP, now we want is that once we tap on the correct letter something appears and let us now that was the correct one. (FOLLOW THE SAME STEPS WE DID BEFORE)


SEARCH THIS OBJECT INSTRUCTION (not allowed on Instagram or facebook)
We have a start icon and “Search this object” we select it and make it a texture sequence.  Add asset and add an animation sequence, then add de texture sequence. 

To the option sender output 0 we link a PULSE and then to the play Animation, on the animation sequence we select CURRENT FRAME and connect it to the progress from the animation. 

This means we will have the play and once we touch it the instructions will pop out.

COUNTDOWN TIMER (this could be also not allowed because of static text)

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


