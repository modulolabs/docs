.. _getting-started-python:


Getting Started with Python
*******************************

The Modulo python API makes it easy to control modulos from a python
program running on computer. When used with python, the modulo controller acts
as a bridge, connecting the modulos to the computer over usb.

Installation
-------------------------------------------------

Mac Installation
_____________________

Install the python libraries by opening a terminal and running::

    sudo easy_install -U modulo-python pyserial

Linux Installation
____________________

Install the python libraries by opening a terminal and running::

    sudo pip install -U modulo-python pyserial


Windows Installation
_____________________

If you are using the Modulo Controller with windows, you'll need to
:ref:`install the driver <windows-driver>`.
A driver is not necessary on mac or linux.

Most windows installations do not come with python, so 
`download <https://www.python.org/downloads/>`_ and install it fist.

Install the python libraries by running::

    pip.exe install -U modulo-python pyserial



Restoring USB Control
--------------------------------------------------------------

If you have previously used the Arduino app with your modulo controller, you'll
need to :ref:`restore the USB Control sketch <restore-usb-control>`. If you
have never used the modulo controller with Arduino you can skip this step.


Running an example program
--------------------------------------------------------------

Now that everything's set up, you can select and run an example program. Depending
on the hardware you have available, choose an example below:

* :ref:`Rainbow Knob Example <example-rainbow-knob-python>` if you have the Knob Modulo.
* :ref:`Joystick and Motor Example <example-joystick-motor-python>` if you have the Joystick and Motor Driver modulos.
* :ref:`Display Example <example-display-python>` if you have the Display modulo.



Listing Devices
--------------------------------------------------------------

Each modulo has a unique number called the Modulo ID. Modulo IDs make it
possible to communicate with a specific modulo, regardless of how it is
physically connected.

You can list all of the connected modulos and their IDs in one of two ways:

1) With a Display Modulo connected and the USB Control sketch running, press
   the right button on the display to page through connected modulos. When a given
   modulo is selected, its type and ID will be display and its LED will blink.
2) The command line program "modulo-list" will list all connected modulos and
   their Modulo IDs. You can also run "modulo-list -i" to interactively
   step through the list of modulos.

   To use modulo-list, the USB Control sketch
   must be running and the python library version 1.0 or greater
   must be installed. (You can update the python library by following the 
   :ref:`installation instructions <getting-started-python>` again.)

You can refer to a specific Modulo in your  program by 
providing its ID when creating the object.
For instance, to automatically use the first Knob::

    knob = modulo.Knob()

And to use the Knob with the ID 12345::

    knob = modulo.Knob(12345)


