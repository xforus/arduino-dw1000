# arduino-dw1000
A library that offers functionality to use Decawave's DW1000 chips/modules with Arduino/AVR
(see http://www.decawave.com/products/dwm1000-module).

Project structure:
 * DW1000 ... contains the Arduino library (which is to be copied to the corresponding libraries folder of your Arduino install or imported via the GUI)
 * DW1000-arduino-test ... contains Arduino test code using the DW1000 library
   * DW1000-arduino-basic-test ... connectivity test
   * DW1000-arduino-sender-test ... sender part of the basic sender/receiver test
   * DW1000-arduino-receiver-test ... receiver part of the basic sender/receiver test
 * DW1000-unit-test ... contains plain C++ unit test code for the library
 * AdapterBoard ... contains PCB files for a 1/10 inch adapter board for the DW1000 module

Project status: 40%

Current milestone: Stable RX/TX between two chips; planned till beginning of June

What works so far:
 * Basic SPI read/write with the chip
 * Fetching of chip configuration and device id
 * Simple IRQ handing
 * Writing of chip configuration
 * Writing of network/node id
 * Writing of transmit data and transmit controls
 * Reading received data
 * Transmission and reception sessions
 * Transmission of packets between two chips (nearly stable)

Next on the agenda:
 * Stable and fast basic transmit and receive
 * Different setups and performance benchmarks
 * Ranging and simple communication examples
 * ...

Usage will be something like:
```
DW1000 dw = DW1000(cs_pin, rst_pin);
dw.initialize();
attachInterrupt(...);
...
dw.newConfiguration();
// configure specific aspects or choose defaults
dw.setDefaults();
dw.interruptOnSent(true);
// .. and other stuff.
dw.commitConfiguration();
...
dw.newTransmit();
// configure specific aspects or choose defaults
dw.setDefaults();
dw.setData(some_data);
dw.startTransmit();
...
// similar for receiving plus IRQ handling
```

A configuration API doc will follow shortly.

The adapter board has the following pin mapping:

Pin | Function
----| ---------
1 (EXTON) | see DW1000 manual
2 (WAKEUP) | see DW1000 manual
3 (RSTn) | Resetting the chip (by pulling low)
4 (GPIO7) | see DW1000 manual
5 (VDD) | 3.3V power supply
6 (GPIO6) | see DW1000 manual
7 (GPIO5) | see DW1000 manual
8 (GPIO4) | see DW1000 manual
9 (GPIO3) | see DW1000 manual
10 (GPIO2) | see DW1000 manual
11 (GPIO1) | see DW1000 manual
12 (GPIO0) | see DW1000 manual
13 (SPICSn) | SPI chip select line (pulling low to activate chip)
14 (SPIMOSI) | SPI communication towards chip
15 (SPIMISO) | SPI communication towards controller
16 (SPICLK) | SPI clock (at most 3MHz in init phase, afterwards up to 20MHz)
17 (GPIO8) | interrupt asserted line, see DW1000 manual
18 (GND) | Ground
