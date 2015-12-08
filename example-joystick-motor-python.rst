.. _example-joystick-motor-python:

Joystick and Motor Example (Python)
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

Save this code to a file called "motor.py", then from a terminal run
"python motor.py". Press Ctrl+C to stop the program.

.. code-block:: python

    # Import the modulo python library
    import modulo

    # Create a new Port object using the first Modulo Controller it finds.
    port = modulo.Port()

    # Create a MotorDriver object attached to the port
    motorDriver = modulo.MotorDriver(port)

    # Create a Joystick object attached to the port
    joystick = modulo.Joystick(port)

    # Run this loop until the program is terminated
    while True :
        # Call port.loop() on each iteration to process events
        port.loop()

        # Get the horizontal and vertical position of the joystick
        # These values will be between -1 and 1
        hpos = joystick.getHPos()
        vpos = joystick.getVPos()

        # Set the speed of the left and right motors
        motorDriver.setMotorA(vpos + hpos)
        motorDriver.setMotorB(vpos - hpos)



Events
==============================================

The approach above works, but constantly checking to the joystick position and
updating the motor speeds isn't very efficient. We can improve upon it using event callbacks.

Event callback are functions that are called automatically when certain events
occur. By registering a callback function we can update the knob's color only
when it is pressed or turned.

Save this code to a file called "motor-events.py", then from a terminal run
"python motor-events.py".

.. code-block:: python

    import modulo

    # This callback function will run whenever the joystick position changes
    def onPositionChanged(joystick) :
        hpos = joystick.getHPos()
        vpos = joystick.getVPos()

        motorDriver.setMotorA(vpos + hpos)
        motorDriver.setMotorB(vpos - hpos)

    # Create a new Port object using the first Modulo Controller it finds.
    port = modulo.Port()

    # Create a MotorDriver object attached to the port
    motorDriver = modulo.MotorDriver(port)

    # Create a Joystick object attached to the port
    joystick = modulo.Joystick(port)

    # Register our callback function
    joystick.positionChangeCallback = onPositionChanged

    # Process events until the program is terminated.
    port.runForever()



