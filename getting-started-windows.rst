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

Windows Driver Tutorial Feedback
-----------------------------------------------

We are interested in gathering feedback on this page. If you used these
instructions please email hello@modulo.co and let us know:

* What version of windows you are using
* If these instructions were accurate and sufficient.
* If you had to do anything that deviated from these instructions


