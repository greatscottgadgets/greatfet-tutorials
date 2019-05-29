Using GreatFET on windows

### Python
* Download the latest version of python3 [here](https://www.python.org/downloads/windows/)
* Be sure to check the `Add Python x.x to PATH` box in the bottom left corner
* Open a command prompt window and type `python -V` to verify that the version of python you downloaded has been installed correctly

### Git
* Download the latest version of git for Windows [here](https://git-scm.com/downloads)

  **Note: the commands described later will be linux-like and done inside the Git bash window instead of the default cmd for Windows**

### Zadig
* Download the latest version of Zadig [here](https://zadig.akeo.ie/)
* We rely on one of the generic USB drivers for Windows; which often needs a little help to wind up installed and bound to the relevant device. For now, the easiest way to do that is to use the Zadig utility to bind the "libusb-win32" driver to the GreatFET device. There's a generic tutorial [here](https://github.com/pbatard/libwdi/wiki/Zadig); you'll need to select the GreatFET device and select "libusb-win32" as the driver to bind to.

### GreatFET
* Go to the [greatfet repo](https://github.com/greatscottgadgets/greatfet) to get the latest source code
* Click  the `clone or download` button in the top right corner and copy the SSH or HTTPS link to your clipboard
* Open a new git bash window (close any existing one if you have one open) and enter the following commands: 
```
git clone [link-copied-above]
cd greatfet
git submodule init
git submodule update
pushd libgreat/host/
python setup.py build
sudo python setup.py install
popd

pushd host/
python setup.py build
sudo python setup.py install
popd
```
* The greatfet host tools should now be installed properly, enter the command `gf info.exe` to verify that a GreatFET One board is found
* **TODO: flashing firmware on Windows**
* The rest of the [Getting Started Guide](https://github.com/greatscottgadgets/greatfet-tutorials/blob/master/getting-started.md#blinking-an-led) can be followed to blink an LED on your GreatFET

**Note: greatfet commands will need `.exe` appended to them; for example `gf shell` in the guide becomes `gf shell.exe`**
