## General-Purpose Input/Output (GPIO)

In the Getting Started with GreatFET tutorial, we blinked one of the built-in
LEDs.  Now let's learn how to manipulate General-Purpose Input/Output (GPIO)
pins so that we can interface with external LEDs or other devices!

You'll need a few things to follow this tutorial:

* GreatFET One (also known as Azalea)
* Solderless Breadboard Neighbor for GreatFET (also known as Daffodil) or any breadboard
* a through-hole LED
* a current-limiting resistor (any value from 200 ohms to 2000 ohms should be fine)


### Controlling an external LED

Connect the LED

Plug the shorter lead of the LED into pin 1 on header J1 and the longer lead of
the LED into a breadboard.  Plug one lead of the resistor into the same row of
the breadboard, and plug its other lead int pin 4 on header J1.

FIXME photo

Open an interactive Python shell:

gf shell FIXME what happens if you don't have IPython installed?

Select a pin by number:

```python
pin = gf.gpio.get_pin('J1_P4')
```

Configure the pin as an output:

```python
pin.set_direction(gf.gpio.DIRECTION_OUT)
```

Turn on the LED:

```python
pin.write(True)
```

Turn off the LED:

```python
pin.write(False)
```

Blink the LED:

```python
import time
for i in range(10):
	pin.write(not pin.read())
	time.sleep(0.2)
```


### GPIO input

Configure the pin as an input:

```python
pin.set_direction(gf.gpio.DIRECTION_IN)
```

Disconnect the LED and use the resistor to connect pin 4 to pin 1 on header J1.
This connects the input to GND (0 V).

```python
pin.read()
```

The read() method should return False, indicating that a low voltage is
connected to the input.

Now disconnect the resistor from pin 1 and connect it to VCC (3.3 V) on pin
2.  It should now connect pin 2 to pin 4 on header J1.

```python
pin.read()
```

The read() method should return True, indicating that a high voltage is
connected to the input.
