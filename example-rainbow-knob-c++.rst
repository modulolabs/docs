.. _example-rainbow-knob-c++:

Rainbow Knob Example (C++)
---------------------------------------------

In this tutorial, we'll make the modulo knob change colors when the knob is
turned. When the knob is pressed, it turns white.

Hardware required:

* Modulo Base (or Modulo Particle Base)
* Controller Modulo (or Particle Photon)
* Knob Modulo

We'll look at two different ways to accomplish this, with polling and events.

Polling
==============================================

The following example uses polling to constantly check the position of the knob
and update the color. It's the simplest way to get the job done.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "KnobTutorial".

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

    // Create an object that represents the knob
    KnobModulo knob;

    // The setup function is run once, when the program starts
    void setup() {
    }

    // The loop function is run constantly
    void loop() {
        // Always call Modulo.loop() at the top of the loop function. It's
        // communicates with the modulos and executes callbacks if any events
        // have occured.
        Modulo.loop();

        // Get the angle of the knob. The angle is between 0 and 360
        float angle = knob.getAngle();

        // Convert the angle (between 0 and 360) to a hue (between 0 and 1)
        float hue = angle/360.0;

        // The saturation is 0 if the button is pressed and 1 otherwise.
        float saturation = 1-knob.getButton();

        // Set the knob's color
        knob.setHSV(hue, saturation, 1.0);
    }


Events
==============================================


The approach above works, but constantly checking to the knob angle and updating
the color isn't very efficient. We can improve upon it using event callbacks.

Event callback are functions that are called automatically when certain events
occur. By registering a callback function we can update the knob's color only
when it is pressed or turned.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "KnobEventsTutorial".

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

    // Declare a function that will be called when the knob is turned or pressed
    void onKnobChanged(KnobModulo &k);

    // Create an object that represents the knob
    KnobModulo knob;

    // The setup function is run once, when the program starts
    void setup() {
        // Attach the callback function to the knob. We're interested in three
        // types of events: button pressed, button release, and position changed.
        knob.setButtonPressCallback(onKnobChanged);
        knob.setButtonReleaseCallback(onKnobChanged);
        knob.setPositionChangeCallback(onKnobChanged);

        // Run the callback once to set the initial color
        onKnobChanged(knob);
    }

    // The loop function is run constantly
    void loop() {
        // Always call Modulo.loop() at the top of the loop function. It
        // communicates with the modulos and executes callbacks.
        //
        // Since we're using events, that's all that needs to happen in loop()!
        Modulo.loop();
    }

    // This is our callback function. It will run when the knob is presed or turned.
    void onKnobChanged(KnobModulo &k) {
        // Get the angle of the knob. The angle is between 0 and 360
        float angle = k.getAngle();

        // Convert the angle (between 0 and 360) to a hue (between 0 and 1)
        float hue = angle/360.0;

        // The saturation is 0 if the button is pressed and 1 otherwise.
        float saturation = 1-k.getButton();

        // Set the knob's color
        k.setHSV(hue, saturation, 1.0);
    }

