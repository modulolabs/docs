.. _windows-driver:

Installing Windows Drivers
===================================

Using the Modulo Controller with windows requires the installation of a driver.
A driver is not required on Mac or Linux.

First, download the driver: `modulo.inf <http://files.modulo.co/modulo.inf>`_.


Windows 7, Vista, and XP
------------------------------------

* When you connect the modulo controller to your computer, windows should
  launch the hardware installer. If it doesn't, open the device manager 
  (Start>Control Panel>Hardware) and find the Modulo Controller. Right click and
  choose **Update Driver Software**.
* When asked **How do you want to search for driver software?**, choose **Browse
  my computer for driver software**.
* Browse to the directory containing the **modulo.inf** file that you just downloaded.
* After a few moments, windows will tell you that it has finished installing the driver.

Windows 8 and 10
------------------------------------------

* If you are using Windows 8, 8.1, or 10 you must disable driver
  signature enforcement before installing the driver. To do so, follow 
  `these instructions <https://learn.sparkfun.com/tutorials/disabling-driver-signature-on-windows-8>`_.

* Next, right click on modulo.inf and select **Install** to complete the driver
  installation.

In some cases this may not correctly associate the driver with with the device.
Open the Device Manager and look for "Modulo Controller" under "Ports". If it's
not there, then

* With the "Unknown Device" icon selected "Update Driver Software..."
* Select "Browse my computer for driver software"
* Select "Let me pick from a list of device drivers on my computer"
* Select "Ports (COM & LPT)" as the device type
* Select "Modulo Labs LLC" as the manufacturer and "Modulo Controller" as the Model.
* It will warn you about updating unverified drivers. Press "YES"

Under "Ports (COM & LPT)" it should now show "Modulo Controller" and the port number.

Cygwin and Python
------------------------------------------

When using python under cygwin, automatic port detection does not work correctly.
Instead you must specify the port path explicitly when creating the Port object.

First, find the port path. if your windows COM port is COM(#), then your virtual
port on cygwin is /dev/ttyS(#-1). (For instance if your Modulo Controller is COM3,
the path to the virtual port is /dev/ttyS2.) You can also find it by running
'ls /dev/ttyS*' in the cygwin terminal.

Once you have found the port path, change the code to use that specific port.
So if your modulo controller is on COM3, then instead of::

    port = modulo.Port()

do::

    port = modulo.Port(serialPortPath="/dev/ttyS2")



Windows Driver Tutorial Feedback
-----------------------------------------------

We are interested in gathering feedback on this page. If you used these
instructions please email hello@modulo.co and let us know:

* What version of windows you are using
* If these instructions were accurate and sufficient.
* If you had to do anything that deviated from these instructions


