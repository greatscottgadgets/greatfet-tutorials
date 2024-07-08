Using GreatFET on windows

### Python
* Download the latest version of python3 [here](https://www.python.org/downloads/windows/)
* Be sure to check the `Add Python x.x to PATH` box in the bottom left corner
![python_installer](images/python_install_box.png)
* Open a command prompt window and type `python -V` to verify that the version of python you downloaded has been installed correctly

![python_version](images/python_version.png)

### Git
* Download the latest version of git for Windows [here](https://git-scm.com/downloads)

### Zadig
* Download the latest version of Zadig [here](https://zadig.akeo.ie/)
* We rely on one of the generic USB drivers for Windows; which often needs a little help to wind up installed and bound to the relevant device. For now, the easiest way to do that is to use the Zadig utility to bind the "libusb-win32" driver to the GreatFET device. There's a generic tutorial [here](https://github.com/pbatard/libwdi/wiki/Zadig); you'll need to select the GreatFET device and select "libusb-win32" as the driver to bind to.

![zadig_window](images/zadig_install_config.png)

* If there is more than one instance of GreatFET in Zadig (e.g., one for Interface 0 and one for Interface 1), the driver needs to be set at the "composite" level.  By default, Zadig hides the composite devices (as Windows will automatically assign it the usbccgp.sys driver).  First select Options and then enable List All Devices.  Select Options again and then disable Ignore Hubs or Composite Parents.  Then find the GreatFET composite entry and assign the relevant USB driver to the composite device (additional note, "libusbk" has been reported as working better than "libusb-win32" by some).

### GreatFET
* Open a new command prompt (close any existing one if you have one open) and enter ```pip install greatfet```

**Note: if you're reading this before the software release, you may need to install the host tools from source. Instructions on how to do so can be found [here](https://github.com/greatscottgadgets/greatfet/wiki/Getting-Started-with-Firmware-Development#installing-host-tools)**
* The greatfet host tools should now be installed properly, enter the command `gf info` to verify that a GreatFET One board is found
* **TODO: flashing firmware on Windows**
* The rest of the [Getting Started Guide](https://github.com/greatscottgadgets/greatfet-tutorials/blob/master/getting-started.md#blinking-an-led) can be followed to blink an LED on your GreatFET

