## Inter-Integrated Circuit (I2C)

I2C is a multi-master, multi-slave, half-duplex serial communication protocol that is commonly used for
inter-chip communication; for example between a microcontroller and a sensor. In this tutorial we will use GreatFET One to interface with a
an I2C temperature and humidity sensor, the SI7021 from Silicon Labs.

Many types sensors are available on breakout boards from Adafruit and other websites, the specific part I'm using is the Adafruit Si7021 Temperature & Humidity Sensor Breakout Board
(Product ID: 3251) Depending on the sensor you are using, the commands you will need to send may differ from the example below but the principple and method will remain the same. 

You can use jumper wires to connect a breakout board to the following pins on GreatFET One:

* clock: J2 pin 40 (SCL)
* data: J2 pin 39 (SDA)
* VCC (5.0 V): J2 pin 2
* GND (ground): J2 pin 1

Before opening a shell we can use the i2c scan utility to determine the I2C address of the sensor:

```terminal
gf i2c --scan
```

This returns a list of working I2C addresses and a table repersenting the address space

```terminal
******** W/R bit set at each valid address ********
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00: W- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: WR -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
```
The 7-bit base slave address of the SI7021 is 0x40, and is read write

Open an interactive Python shell:

```
gf shell
```

before opening a shell we can use the i2c scan utility to determine the I2C address of the sensor:

```python
gf.i2c.scan()
```

Turn it off:

```python
gf.spi.transmit([0x00, 0x00, 0x00, 0x00, 0xff, 0x00, 0x00, 0x00])
```

The spi.transmit() method executes a bi-directional data transfer.  The
GreatFET One acts as SPI master, pulling down SSEL (slave select) to activate
the slave and then driving SCK (SPI clock) and MOSI (master out, slave in).  We
haven't wired up SSEL because the APA102 LEDs do not require it.

As it clocks data out on MOSI, it also clocks in the same amount of data from
the slave on MISO (master in, slave out).  The argument passed to
spi.transmit() is an array of bytes to transmit.  The method returns the
received data as an array of bytes.  The APA102 does not implement
bi-directional communication, so we haven't connected anything to MISO.  That
means that spi.transmit() always returns an array of bytes with all bits set
(0xff) every time we call it, but we can ignore that.

You can paste the following program into your shell to see a fancy light show!

```python
import bitstring
import time
import math

def led_frame(red=0, green=0, blue=0, brightness=0x1f):
    frame = bitstring.Bits(length=3, uint=0x7)
    frame += bitstring.Bits(length=5, uint=(brightness & 0x1f))
    frame += bitstring.Bits(length=8, uint=(blue & 0xff))
    frame += bitstring.Bits(length=8, uint=(green & 0xff))
    frame += bitstring.Bits(length=8, uint=(red & 0xff))
    return frame

def chase():
    brightness = 1
    length = 60 # set this to the number of LEDs in your strip
    period = length / 2.0
    start_frame = bitstring.Bits('0x00000000')
    pixels = bitstring.BitStream()
    for i in range(length):
        red = int(127+127*math.cos(2*math.pi*(i/period)))
        green = int(127+127*math.cos(2*math.pi*((i+period/3)/period)))
        blue = int(127+127*math.cos(2*math.pi*((i+2*period/3)/period)))
        pixels += led_frame(red, green, blue, brightness)
    while(True):
        gf.spi.transmit((start_frame + pixels).bytes)
        time.sleep(0.02)
        pixels.ror(32) # rotate the pixel array by 32 bits which is one LED

chase()
```
