## Getting Started with GreatFET

Follow these instructions to get started with GreatFET on Linux.


### Install or Update Software

```
sudo pip3 install --upgrade greatfet
```


### Install udev Rules

This is an optional step that we recommend so that you will be able to use your
GreatFET as a non-root user.  The example udev rules file that we provide
assumes that your user is a member of the plugdev group.  If that is not the
case, you can either add your user to the plugdev group or modify the file to
give permission to the group of your choice instead of plugdev.

```
git clone https://github.com/greatscottgadgets/greatfet.git
sudo cp greatfet/host/misc/54-greatfet.rules /etc/udev/rules.d
sudo udevadm control --reload-rules
```


### Connect your GreatFET One

Find the USB0 port on your GreatFET One.  This is the port on the left (convex)
side of the board, the side with LEDs and buttons.  Use a USB cable to connect
this port to your host computer.

### Install Windows Drivers

We rely on one of the generic USB drivers for Windows; which often needs a little help to wind up installed and bound to the relevant device. For now, the easiest way to do that is to use the Zadig utility to bind the "libusb-win32" driver to the GreatFET device. There's a generic tutorial here: https://github.com/pbatard/libwdi/wiki/Zadig; you'll need to select the GreatFET device and select "libusb-win32" as the driver to bind to.

### Check your GreatFET One

Once connected, your GreatFET One should start to slowly flash LED1, indicating
that it is operating.  Confirm that your host computer can communicate with the
GreatFET One by typing:

```
greatfet info
```

This is an example of a command-line tool that is accessible as a subcommand of
the unified "greatfet" command.  The "greatfet" command is also installed as
"gf".  Let's try the abbreviated form:

```
gf info
```

The output of this command shows you information about connected GreatFET
devices.


### Update Firmware

After installing or updating GreatFET software on your host computer it is
important to update the firmware on your GreatFET One to match.  This can be
done with a single command:

```
gf fw --auto
```


### Blinking an LED

There are four fabulous LEDs on GreatFET One.  LED1 normally indicates a
heartbeat, but you can do whatever you like with LED2, LED3, and LED4.  Let's
try blinking an LED from Python.

First start up an interactive Python shell:

```
gf shell
```

The "gf shell" command starts an IPython shell, connects to the first GreatFET
One it finds, and sets up an object called "gf" that you can use to interact
with the GreatFET One.

Try turning on LED2 from the shell:

```python
led = gf.leds[2]
led.toggle()
```

now try blinking LED3 a few times:

```python
import time
for i in range(10):
	gf.leds[3].toggle()
	time.sleep(0.2)
```

That's it!  To get started exploring the Python capabilities of
GreatFET, you can try using the tab key to complete commands or try the
built-in help:

```python
help(gf.leds[3])
```

For bonus points, see if you can turn off the heartbeat and control LED1.
Here's a help command to get you started:

```python
help(gf.apis.heartbeat)
```

When you're ready to try something new, type "exit" to close the Python shell
and check out one of the [other tutorials](README.md)!
