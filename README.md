# urboot.hex
### Pre-compiled [urboot](https://github.com/stefanrueger/urboot/) bootloaders

This repository contains 96,217 *different* pre-compiled bootloaders in the directory tree
[`mcus`](https://github.com/stefanrueger/urboot.hex/tree/main/mcus/) sorted by MCU name, eg,
autobaud bootloaders for the
[ATmega328P](https://github.com/stefanrueger/urboot.hex/blob/main/mcus/atmega328p/autobaud/README.md).

The [`boards`](https://github.com/stefanrueger/urboot.hex/tree/main/boards/) directory contains 
urboot bootloaders sorted by board name. Here one can find, eg, autobaud bootloaders for the
venerable ATmega328P based
[Uno](https://github.com/stefanrueger/urboot.hex/blob/main/boards/uno/autobaud/README.md) that
has an LED on PB5, the [Pro
Mini](https://github.com/stefanrueger/urboot.hex/tree/main/boards/promini/autobaud/README.md)
(same bootloaders), the
[Jeenode](https://github.com/stefanrueger/urboot.hex/tree/main/boards/jeenode/autobaud/README.md)
board with a low-active LED on PB1, the ATmega1284P based [Moteino
Mega](https://github.com/stefanrueger/urboot.hex/tree/main/boards/moteinomega/autobaud/README.md)
and the ATmega2560 [Mega R3
board](https://github.com/stefanrueger/urboot.hex/tree/main/boards/mega-r3/autobaud/README.md). The `boards`
directory also contains fixed baud rate bootloaders, eg, some 16 MHz and 115,200 baud bootloaders for the ATtiny167 based [Digispark
Pro](https://github.com/stefanrueger/urboot.hex/tree/main/boards/digispark-pro/fcpu_16mhz/115200_bps/README.md),
the ATtiny85 based
[Disgispark](https://github.com/stefanrueger/urboot.hex/tree/main/boards/digispark/fcpu_16mhz/115200_bps/README.md)
and the ATtiny84 based
[Luminet](https://github.com/stefanrueger/urboot.hex/tree/main/boards/luminet/fcpu_16mhz/115200_bps/README.md).

Finally, there are pre-compiled urboot bootloaders for popular Arduino cores in the
[`cores`](https://github.com/stefanrueger/urboot.hex/tree/main/cores) directory of the
[urboot.hex](https://github.com/stefanrueger/urboot.hex) repository. The pre-compiled .hex
bootloaders of the `boards` and `cores` directories are copies of selected relevant bootloaders
in the `mcus` tree, typically engaging the correct activity LED for visual feedback while the
bootloader is active. With these bootloaders the board LED comes on after an external reset of
the board at the beginning of each character read `getc()` routine and is switched off at the end
of each `getc()`. When the bootloader times out at the end of its engagement the LED is switched
off (unless, of course, it is used thereafter in the uploaded application). There is no need to
select a bootloader with [blinkenlights](https://en.wikipedia.org/wiki/Blinkenlights): a silent
bootloader from the corresponding `mcus` tree which has either `_lednop` or no `_led`  in the
filename would equally be suitable for the board/core in consideration.


The `mcus` tree actually contains 234,168 .hex files, but these are somewhat redundant because a
bootloader on 115,200 baud for 16 MHz is *exactly* the same as a bootloader on 57,600 baud for 8
MHz. All in all, some 935,564 bootloaders were originally created for this repository, but the
majority of bootloaders could be removed because they turned out to be superseded by another one
with more features that occupies the same space and would therefore be preferred.

Click on the links below to get more information about 
 - The [urboot](https://github.com/stefanrueger/urboot/) project
 - Its [background](https://github.com/stefanrueger/urboot/blob/main/docs/background.md)
 - [Compiling](https://github.com/stefanrueger/urboot/blob/main/README.md#compiling) your own bootloader using urboot [make options](https://github.com/stefanrueger/urboot/blob/main/docs/makeoptions.md)
 - [Selecting](https://github.com/stefanrueger/urboot/blob/main/docs/howtoselect.md) the right bootloader for you
 - [Using](https://github.com/stefanrueger/urboot/blob/main/README.md#usage) them
 - How they [compare](https://github.com/stefanrueger/urboot/blob/main/README.md#comparison) to optiboot
 - And, finally, how to [trouble-shoot](https://github.com/stefanrueger/urboot/blob/main/README.md#trouble-shooting) them if things go wrong
