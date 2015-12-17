.. _example-joystick-motor-c++:

Joystick and Motor Example (C++)
---------------------------------------------

In this tutorial, we'll use use the joystick to control the speed and
direction of two DC motors for a small wheeled robot.

Hardware required:

* Modulo Base (or Modulo Particle Base)
* Controller Modulo (or Particle Photon)
* Joystick Modulo
* Motor Driver Modulo
* Two DC motors

We'll look at two different ways to accomplish this, with polling and events.

Polling
==============================================

The following example uses polling to constantly check the position of the
joystick and update the motor speed. It's the simplest way to get the job done.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "MotorTutorial".

.. code-block:: c++

    // For Arduino, include the Modulo library and the Wire library, which it depends on.
    #ifdef ARDUINO
    #include "Modulo.h"
    #include "Wire.h"
    #endif

    // For Particle, include the Modulo library.
    #ifdef PARTICLE
    #include "Modulo/Modulo.h"
    #endif

    // Create an object that represents each modulo
    MotorDriverModulo motorDriver;
    JoystickModulo joystick;

    // The setup function is run once, when the program starts
    void setup() {
    }

    // The loop function is run constantly
    void loop() {
        // Always call Modulo.loop() at the top of the loop function. It
        // communicates with the modulos and executes callbacks if any events
        // have occured.
        Modulo.loop();

        // Get the horizontal and vertical position if the joystick
        float hpos = joystick.getHPos();
        float vpos = joystick.getVPos();

        // Set the speed of motor A. 
        motorDriver.setMotorA(vpos + hpos);
        motorDriver.setMotorB(vpos - hpos);
    }


Events
==============================================

The approach above works, but constantly checking to the joystick position and
updating the motor speeds isn't very efficient. We can improve upon it using event callbacks.

Event callback are functions that are called automatically when certain events
occur. By registering a callback function we can update the knob's color only
when it is pressed or turned.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "MotorEventsTutorial".

.. code-block:: c++

    // For Arduino, include the Modulo library and the Wire library, which it depends on.
    #ifdef ARDUINO
    #include "Modulo.h"
    #include "Wire.h"
    #endif

    // For Particle, include the Modulo library.
    #ifdef PARTICLE
    #include "Modulo/Modulo.h"
    #endif

    // Create an object that represents each modulo
    MotorDriverModulo motorDriver;
    JoystickModulo joystick;

    // Declare a function that will be called when the joystick moves
    void onJoystickChanged(JoystickModulo &k);


    // The setup function is run once, when the program starts
    void setup() {

    }

    // The loop function is run constantly
    void loop() {
        // Always call Modulo.loop() at the top of the loop function. It
        // communicates with the modulos and executes callbacks.
        //
        // Since we're using events, that's all that needs to happen in loop()!
        Modulo.loop();
    }

    void onJoystickChanged(JoystickModulo &j) {
        // Get the horizontal and vertical position if the joystick
        float hpos = j.getHPos();
        float vpos = j.getVPos();

        // Set the speed of motor A. 
        motorDriver.setMotorA(vpos + hpos);
        motorDriver.setMotorB(vpos - hpos);
    }

