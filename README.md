# urboot.hex
### Pre-compiled [urboot](https://github.com/stefanrueger/urboot/) bootloaders

This repository contains 33,779 *different* pre-compiled bootloaders in the directory trees
[`mcus`](https://github.com/stefanrueger/urboot.hex/tree/main/mcus/) sorted by MCU name, eg,
autobaud bootloaders for the
[ATmega328P](https://github.com/stefanrueger/urboot.hex/blob/main/mcus/atmega328p/autobaud/README.md), and
[`boards`](https://github.com/stefanrueger/urboot.hex/tree/main/boards/) sorted by board name, eg,
autobaud bootloaders for the venerable ATmega328P based
[Uno](https://github.com/stefanrueger/urboot.hex/blob/main/boards/uno/autobaud/README.md)
with a LED on PB5, the [Arduino Pro
Mini](https://github.com/stefanrueger/urboot.hex/tree/main/boards/promini/autobaud/README.md)
(same bootloaders), the
[Jeenode](https://github.com/stefanrueger/urboot.hex/tree/main/boards/jeenode/autobaud/README.md)
with a low-active LED on PB1, the ATmega1284P based [Moteino
Mega](https://github.com/stefanrueger/urboot.hex/tree/main/boards/moteinomega/autobaud/README.md)
and the ATmega2560 [Mega R3
board](https://github.com/stefanrueger/urboot.hex/tree/main/boards/mega-r3/autobaud/README.md);
or, eg, some 16 MHz and 115,200 baud bootloaders for the [ATtiny167 based Digispark
Pro](https://github.com/stefanrueger/urboot.hex/tree/main/boards/digispark-pro/fcpu_16mhz/115200_bps/README.md),
the [ATtiny85 based
Disgispark](https://github.com/stefanrueger/urboot.hex/tree/main/boards/digispark/fcpu_16mhz/115200_bps/README.md)
and the [ATtiny84 based
Luminet](https://github.com/stefanrueger/urboot.hex/tree/main/boards/luminet/fcpu_16mhz/115200_bps/README.md).

The trees actually contain 98,564 hex files, but they are somewhat
redundant because a bootloader on 115,200 baud for 16 MHz is *exactly* the
same as a bootloader on 57,600 baud for 8 MHz.

Click on the links below to get more information about 
 - The [urboot](https://github.com/stefanrueger/urboot/) project
 - Its [background](https://github.com/stefanrueger/urboot/blob/main/docs/background.md)
 - [Compiling](https://github.com/stefanrueger/urboot/blob/main/README.md#compiling) your own bootloader using urboot [make options](https://github.com/stefanrueger/urboot/blob/main/docs/makeoptions.md)
 - [Selecting](https://github.com/stefanrueger/urboot/blob/main/docs/howtoselect.md) the right bootloader for you
 - [Using](https://github.com/stefanrueger/urboot/blob/main/README.md#usage) them
 - How they [compare](https://github.com/stefanrueger/urboot/blob/main/README.md#comparison) to optiboot
 - And, finally, how to [trouble-shoot](https://github.com/stefanrueger/urboot/blob/main/README.md#trouble-shooting) them if things go wrong
