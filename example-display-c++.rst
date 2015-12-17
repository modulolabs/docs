.. _example-display-c++:

Display Example (C++)
---------------------------------------------

In this tutorial, we'll display different things on the Modulo display based on
which button is pressed.

We'll look at two different ways to accomplish this, with polling and events.

Hardware required:

* Modulo Base (or Modulo Particle Base)
* Controller Modulo (or Particle Photon)
* Display Modulo

Polling
==============================================

The following example uses polling to constantly check the state of the buttons
and draw different things. It's the simplest way to get the job done.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "DisplayTutorial".

::

    // For Arduino, include the Modulo library and the Wire library, which it depends on.
    #ifdef ARDUINO
    #include "Modulo.h"
    #include "Wire.h"
    #endif

    // For Particle, include the Modulo library.
    #ifdef PARTICLE
    #include "Modulo/Modulo.h"
    #endif

    // Create an object that represents the display
    DisplayModulo display;

    // The setup function is run once, when the program starts
    void setup() {
    }

    // The loop function is run constantly
    void loop() {
        // Always call Modulo.loop() at the top of the loop function. It
        // communicates with the modulos and executes callbacks if any events
        // have occured.
        Modulo.loop();

        // Clear the display
        display.clear();

        // Draw different text, in a different color, based on which button is pressed.
        if (display.getButton(0)) {
            display.setTextColor(255,0,0);
            display.println("Button 0");
        } else if (display.getButton(1)) {
            display.setTextColor(0,255,0);
            display.println("Button 1");
        } else if (display.getButton(2)) {
            display.setTextColor(0,0,255);
            display.println("Button 2");
        } else {
            display.setTextColor(255,255,255);
            display.println("None pressed");        
        }

        // Nothing will actually show up on the display until you call refresh.
        display.refresh();
    }

Events
==============================================

The approach above works, but constantly checking to the buttons and redrawing
the screen isn't very efficient. We can improve upon it using event callbacks.

Event callback are functions that are called automatically when certain events
occur. By registering a callback function we can update the display only when
a button is pressed or released.

Run this program in the Arduino app by going to the "Arduino > Examples > Modulo"
menu and selecting "DisplayEventsTutorial".

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

    // Create an object that represents the display
    DisplayModulo display;

    // Declare a function that will be called when a button is pressed
    void onButtonPress(DisplayModulo &d, int button);

    // Declare a function that will be called when a button is release
    void onButtonRelease(DisplayModulo &d, int button);


    // The setup function is run once, when the program starts
    void setup() {
        display.setButtonPressCallback(onButtonPress);
        display.setButtonReleaseCallback(onButtonRelease);

        // Call onButtonRelease to draw the initial text
        onButtonRelease(display, 0);
    }

    // The loop function is run constantly
    void loop() {
        // Always call Modulo.loop() at the top of the loop function. It
        // communicates with the modulos and executes callbacks.
        //
        // Since we're using events, that's all that needs to happen in loop()!
        Modulo.loop();
    }

    // This callback function will run when a button is pressed.
    void onButtonPress(DisplayModulo &d, int button) {
        // Clear the display
        display.clear();

        // Draw different text, in a different color, based on which button is pressed.
        switch (button) {
            case 0:
                display.setTextColor(255,0,0);
                display.println("Button 0");
                break;
            case 1:
                display.setTextColor(0,255,0);
                display.println("Button 1");
                break;
            case 2:
                display.setTextColor(0,0,255);
                display.println("Button 2");
                break;
        }

        // Nothing will actually show up on the display until you call refresh.
        display.refresh();
    }

    void onButtonRelease(DisplayModulo &d, int button) {
        // Clear the display
        display.clear();

        // Write "none pressed" in white.
        display.setTextColor(255,255,255);
        display.println("None pressed");        

        display.refresh();
    }


