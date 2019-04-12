## Serial Peripheral Interface (SPI)

SPI is a full-duplex serial communications protocol that is commonly used for
inter-chip communication such as the interface between a microcontroller and
flash memory.  In this tutorial we will use GreatFET One to interface with a
SPI flash device.

FIXME find a SPI DIP

Plug the target chip into a breadboard and use jumper wires to connect it to
the following pins on GreatFET One:

* SSEL (slave select): J1 pin 37
* SCK (SPI clock): J1 pin 38
* MOSI (master out, slave in): J1 pin 39
* MISO (master in, slave out): J1 pin 40
* VCC (3.3 V supply): J1 pin 2
* GND (ground): J1 pin 1
FIXME WP or other pins?

FIXME photo

Open an interactive Python shell:

```
gf shell
```

```python
gf.spi.transmit([0x9f, 0x00, 0x00, 0x00])
```

The spi.transmit() method executes a bi-directional data transfer.  The
GreatFET One acts as SPI master, pulling down SSEL to activate the slave and
then driving SCK and MOSI.  As it clocks data out on MOSI, it also clocks in
the same amount of data from the slave on MISO.  The argument passed to
spi.transmit() is an array of bytes to transmit.  The method returns the
received data as an array of bytes.

In this example, we transmit 0x9f which is a standard command for SPI flash
devices that asks the slave for information about itself.  Additionally we
clock out three bytes that are ignored by the slave but which are required in
order to clock in the slave's response.  The slave's transmits a total of four
bytes, including a three byte response starting on the second byte (after the slave has received the command which was transmitted k


```python
gf.spi.transmit([0x9f], 4)
```



FIXME gf spiflash
