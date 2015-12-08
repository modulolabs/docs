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

Running an example program
--------------------------------------------------------------

Now that everything's set up, you can select and run an example program. Depending
on the hardware you have available, choose an example below:

* :ref:`Rainbow Knob Example <example-rainbow-knob-c++>` if you have the Knob Modulo.
* :ref:`Joystick and Motor Example <example-joystick-motor-c++>` if you have the Joystick and Motor Driver modulos.
* :ref:`Display Example <example-display-c++>` if you have the Display modulo.


