.. _example-rainbow-knob-python:

Rainbow Knob Example (Python)
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

Save this code to a file called "knob.py", then from a terminal run
"python knob.py".

.. code-block:: python

    # Import the modulo python library
    import modulo

    # Create a new Port object using the first Modulo Controller it finds.
    port = modulo.Port()

    # Create a Knob object attached to the port
    knob = modulo.Knob(port)

    # Run this loop until the program is terminated
    while True :
        # Call port.loop() on each iteration to process events
        port.loop()

        # Get the angle of the knob (between 0 and 360)
        angle = knob.getAngle()

        # Divide the angle by 360 to get the hue, which is between 0 and 1
        hue = angle/360.0

        # When the knob is pressed, set the saturation to 0.
        saturation = 1-knob.getButton()

        # Set the color. The value is always 1.0 (full brightness)
        knob.setHSV(hue, saturation, 1.0)


Events
==============================================


The approach above works, but constantly checking to the knob angle and updating
the color isn't very efficient. We can improve upon it using event callbacks.

Event callback are functions that are called automatically when certain events
occur. By registering a callback function we can update the knob's color only
when it is pressed or turned.

Save this code to a file called "knob-events.py", then from a terminal run
"python knob-events.py".

.. code-block:: python

    # Import the modulo python library
    import modulo

    # This callback function will run whenever the knob position changes
    def onPositionChanged(knob) :
        # Get the angle of the knob (between 0 and 360)
        angle = knob.getAngle()

        # Divide the angle by 360 to get the hue, which is between 0 and 1
        hue = angle/360.0

        # When the knob is pressed, set the saturation to 0.
        saturation = 1-knob.getButton()

        # Set the color. The value is always 1.0 (full brightness)
        knob.setHSV(hue, saturation, 1.0)

    # Create a new Port object using the first Modulo Controller it finds.
    port = modulo.Port()

    # Create a Knob object attached to the port
    knob = modulo.Knob(port)

    # Register our callback function
    knob.positionChangeCallback = onPositionChanged

    # Process events until the program is terminated.
    port.runForever()


