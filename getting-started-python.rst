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

    sudo easy_install modulo-python pyserial

Linux Installation
____________________

Install the python libraries by opening a terminal and running::

    sudo pip install modulo-python pyserial


Windows Installation
_____________________

If you are using the Modulo Controller with windows, you'll need to
:ref:`install the driver <windows-driver>`.
A driver is not necessary on mac or linux.

Most windows installations do not come with python, so 
`download <https://www.python.org/downloads/>`_ and install it fist.

Install the python libraries by running::

    pip.exe install modulo-python pyserial



Restoring USB Control
--------------------------------------------------------------

If you have previously used the Arduino app with your modulo controller, you'll
need to :ref:`restore the USB Control sketch <restore-usb-control>`. If you
have never used the modulo controller with Arduino you can skip this step.


Run an example program
--------------------------------------------------------------

To use modulo from python, connect the Modulo controller to your computer via
USB.

Save the code below to a file called "example.py" and then in a terminal,
run "python example.py" in a terminal::

   import modulo, time

   port = modulo.Port()
   knob = modulo.Knob(port)
   display = modulo.Display(port)

   while True :
       display.clear()
       display.set_cursor(0,0)
       display.writeln(knob.get_angle())
       display.update()
       time.sleep(.05)

Understanding the example
--------------------------------------------------------------

Your code only needs to do three things:

1) Create a Port object to communicate with the hardware.
2) Create an object for each Modulo
3) Call methods on the modulo objects to control them.



