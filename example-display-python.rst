.. _example-display-python:

Display Example (Python)
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

Save this code to a file called "display.py", then from a terminal run
"python display.py". Press Ctrl+C to stop the program.

.. code-block:: python

    # Import the modulo python library
    import modulo

    # Create a new Port object using the first Modulo Controller it finds.
    port = modulo.Port()

    # Create a Display object attached to the port
    display = modulo.Display(port)

    # Run this loop until the program is terminated
    while True :
        # Call port.loop() on each iteration to process events
        port.loop()

        # Clear the display
        display.clear()

        # Draw text to the display. The color and text depend on which
        # button is pressed.
        if display.getButton(0) :
            display.setTextColor(1,0,0)
            print >>display, "Button 0"
        elif display.getButton(1) :
            display.setTextColor(0,1,0)
            print >>display, "Button 1"
        elif display.getButton(2) :
            display.setTextColor(0,0,1)
            print >>display, "Button 2"
        else :
            display.setTextColor(1,1,1)
            print >>display, "Press Button"

        # Call refresh to update the display
        display.refresh()



Events
==============================================

The approach above works, but constantly checking to the buttons and redrawing
the screen isn't very efficient. We can improve upon it using event callbacks.

Event callback are functions that are called automatically when certain events
occur. By registering a callback function we can update the display only when
a button is pressed or released.

Save this code to a file called "display-events.py", then from a terminal run
"python display-events.py".

.. code-block:: python

    # Import the modulo python library
    import modulo

    # This callback function will run any time a button is pressed
    def onButtonPressed(display, button) :
        # First, clear the display
        display.clear()

        # Draw text to the display. The color and text depend on which
        # button was pressed.
        if button == 0:
            display.setTextColor(1,0,0)
            print >>display, "Button 0"
        elif button == 1 :
            display.setTextColor(0,1,0)
            print >>display, "Button 1"
        elif button == 2:
            display.setTextColor(0,0,1)
            print >>display, "Button 2"

        # Call refresh to update the display
        display.refresh()

    # This callback function will run any time a button is pressed
    def onButtonReleased(display, button):
        # First, clear the display
        display.clear()

        # Draw the text "Press Button" in white
        display.setTextColor(1,1,1)
        print >>display, "Press Button"

        # Call refresh to update the display
        display.refresh()

    # Create a new Port object using the first Modulo Controller it finds.
    port = modulo.Port()

    # Create a Display object attached to the port
    display = modulo.Display(port)

    # Register our callback functions
    display.buttonPressCallback = onButtonPressed
    display.buttonReleaseCallback = onButtonReleased

    # Execute the onButtonReleased function to update the display
    onButtonReleased(display, 0)

    # Process events until the program is terminated.
    port.runForever()



