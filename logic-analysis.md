## Logic Analysis

Let's take a look at how we can use GreatFET One as a logic analyzer for 3.3 V
digital signals.  (For I/O voltages other than 3.3 V, you would also need a
level shifter.)

The GreatFET logic analysis function uses a peripheral called SGPIO, so we need
to connect the SGPIO pins to our target signals.  One easy way to find a target
is to use one of the GreatFET's other peripherals such as SPI.

Use jumper wires to make the following connections:

* Connect J1 pin 4 (SGPIO0) to J1 pin 37 (SSEL)
* Connect J1 pin 6 (SGPIO1) to J1 pin 38 (SCK)
* Connect J1 pin 28 (SGPIO2) to J1 pin 39 (MOSI)
* Connect J1 pin 30 (SGPIO3) to J1 pin 40 (MISO)

Open an interactive Python shell in your first terminal window:

```
gf shell
```

FIXME set up SPI


In a second terminal window activate logic analysis:

```
gf logic -p /tmp/spi-capture
```
FIXME file extension?


In the Python shell, type:

```
gf.spi.transmit("GreatFET")
```


In the second window, terminate gf logic by typing ctrl-c.

FIXME open in pulseview

FIXME analyze in pulseview
