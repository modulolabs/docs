Getting Started with Arduino
********************


Download Arduino.
--------------------------------------------------------------
Download and install arduino from arduino.cc. You must use version 1.6.6 or
later. Earlier versions will not work.

Drivers
--------------------------------------------------------------
If you are using the Modulo Controller with windows, you'll need to
install a driver. A driver is not necessary on mac or linux.

:ref:`windows-driver`

Installing the Modulo Controller board package for Arduino
--------------------------------------------------------------

In order to use the Modulo Controller with the Arduino app, you need to install
board support packages.

1) First, open Preferences under the Arduino menu.
2) In Preferences under "Additional Board Manager URLs" add: http://files.modulo.co/package_modulo_index.json
3) Press "OK" to close Preferences.
4) Open "Board Manager" under the "Tools > Board" menu.
5) In the Board Manager install both of these board packages:
    Modulo Controller
    Arduino SAMD Boards


Installing the Modulo Library for Arduino
--------------------------------------------------------------
The Modulo Library makes it easy to work with Modulo whether you're using
the Modulo Controller or some other Arduino board.

To install it:

1. Select "Manage Librarys" under the Sketch > Include Library menu.
2. Search for and select the library "Modulo"
3. Click "Install"

..
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
       must be running and the python library must be installed.

       (NOTE: modulo-list
       is currently broken but will be fixed in the next version of the python
       library.)

Run an example sketch
--------------------------------------------------------------
Once the Modulo library is installed, you can open and run an example sketch!

1. From the File > Examples > Modulo menu, select an example sketch
2. Make sure that "Modulo Controller" is selected under the Tools > Board menu.
3. Make sure that the correct port is selected under under the Tools > Port menu.
4. Press the Upload button to run the sketch!

Sometimes the Arduino app is not able to reset the controller into bootloader
mode, which causes the upload to fail. (This seems to happen frequently on
OSX El Capitan). You can avoid that problem by double-tapping the Controller's
reset button (to manually enter bootloader mode) before clicking 'Upload'.

.. _restore-usb-control:

Restore USB Control Sketch
--------------------------------------------------------------

When you first receive your Modulo Controller it's loaded with a program that
lets it be controlled from python over USB. If you have uploaded a different
program with the Arduino app, you won't be able to use it with python anymore.

Fortunately, it's easy to restore the original USB Control program. Just open
and run the "USB Control" sketch from the File > Examples > Modulo menu.

