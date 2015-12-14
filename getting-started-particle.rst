Getting Started with Particle
***********************************

Modulo works great with the Photon and Core. Particle provides two IDEs that
you can use. `Particle Build <http://build.particle.io>`_ is a web based IDE,
and `Particle Dev <https://www.particle.io/dev>`_ is a desktop IDE.

If you haven't worked with them before, follow the getting started tutorial
in the `Particle Docs <https://docs.particle.io>`_ before continuing.

Using Modulo with Particle Build (the online IDE)
--------------------------------------------------------------

In Particle Build, you can include the Modulo library by searching for it
in the Libraries tab and clicking "Include in App". This will also Include
the Modulo library in your project's .ino file this::

    #include "Modulo/Modulo.h"

Using Modulo with Particle Dev (the desktop IDE)
--------------------------------------------------------------

When using particle dev, you must put a copy of the Modulo library in the same
directory as your project source code.

Download the latest version of the `Modulo Library <https://github.com/modulolabs/modulo-lib/releases>`_.

Copy or link the "firmware" subdirectory to the directory containing your project.
Do NOT copy the entire downloaded directory into your project, only the "firmware" subdirectory.

So your files will be::

    MyProject/
        MyProject.cpp
        Modulo/   (This is the 'firmware' subdirectory from the modulo lib)
            Modulo.h
            <other Modulo library files>

Despite the fact that the modulo library files are in a "Modulo" subdirectory,
Particle Dev flattens everythings out when it builds your project. Because of
that, your #include must be for "Modulo.h", not "Modulo/Modulo.h"::

    #include "Modulo.h"

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

Running an example program
--------------------------------------------------------------

Now that everything's set up, you can select and run an example program. Depending
on the hardware you have available, choose an example below:

* :ref:`Rainbow Knob Example <example-rainbow-knob-c++>` if you have the Knob Modulo.
* :ref:`Joystick and Motor Example <example-joystick-motor-c++>` if you have the Joystick and Motor Driver modulos.
* :ref:`Display Example <example-display-c++>` if you have the Display modulo.


