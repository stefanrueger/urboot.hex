# urboot.hex
### Pre-compiled `u8.0` [urboot](https://github.com/stefanrueger/urboot/) bootloaders

This repository contains pre-compiled AVR bootloaders to be used with the `avrdude -c urclock`
uploader. They are all in the directory tree
[`mcus`](https://github.com/stefanrueger/urboot.hex/tree/main/mcus/) sorted by MCU name, eg,
autobaud bootloaders for the
[ATmega328P](https://github.com/stefanrueger/urboot.hex/blob/main/mcus/atmega328p/watchdog_1_s/autobaud/uart0_rxd0_txd1/no-led/README.md).

The [`boards`](https://github.com/stefanrueger/urboot.hex/tree/main/boards/) directory contains
urboot bootloaders sorted by board name. Here one can find, eg, autobaud bootloaders for the
venerable ATmega328P based
[Uno](https://github.com/stefanrueger/urboot.hex/blob/main/boards/uno/atmega328p/watchdog_1_s/autobaud//uart0_rxd0_txd1/led+b5/README.md)
with a LED on PB5, the [Arduino Pro
Mini](https://github.com/stefanrueger/urboot.hex/tree/main/boards/promini/atmega328p/watchdog_1_s/autobaud/uart0_rxd0_txd1/led+b5/README.md)
(same bootloaders), the
[Jeenode](https://github.com/stefanrueger/urboot.hex/tree/main/boards/jeenode/atmega328p/watchdog_1_s/autobaud/uart0_rxd0_txd1/led-b1/README.md)
with a low-active LED on PB1, the ATmega1284P based [Moteino
Mega](https://github.com/stefanrueger/urboot.hex/tree/main/boards/moteinomega/atmega1284p/watchdog_1_s/autobaud/uart0_rxd0_txd1/led+d7/README.md)
and the ATmega2560 [Mega R3
board](https://github.com/stefanrueger/urboot.hex/tree/main/boards/mega-r3/atmega2560/watchdog_1_s/autobaud/uart0_rxe0_txe1/led+b7/README.md);
or, eg, some 16 MHz and 115,200 baud bootloaders for the [ATtiny167 based Digispark
Pro](https://github.com/stefanrueger/urboot.hex/tree/main/boards/digispark-pro/attiny167/watchdog_1_s/external_oscillator_x/16m000000_hz/+115k2_baud/uart0_rxa0_txa1/led+b1/README.md),
the [ATtiny85 based
Disgispark](https://github.com/stefanrueger/urboot.hex/tree/main/boards/digispark/attiny85/watchdog_1_s/external_oscillator_x/16m000000_hz/+115k2_baud/swio_rxb4_txb3/led+b1/README.md)
and the [ATtiny84 based
Luminet](https://github.com/stefanrueger/urboot.hex/tree/main/boards/luminet/attiny84/watchdog_1_s/external_oscillator_x/16m000000_hz/+115k2_baud/swio_rxa3_txa2/led+a4/README.md).

Finally, there are pre-compiled urboot bootloaders for popular Arduino cores in the
[`cores`](https://github.com/stefanrueger/urboot.hex/tree/main/cores) directory. 

There is a subtle distinction between bootloaders for MCUs driven by an *external* oscillator,
which tend to have a small (< 0.2%) deviation from the nominal F<sub>CPU</sub>, and MCUs running on
an *internal* oscillator, which more often than not exhibit a deviation of 2% or more from the
nominal clock frequency. For the former, the pre-compiled urboot bootloaders tend to be shorter and
faster at the cost of potentially higher quantisation errors for the baud rate, up to 2.1%. For the
latter the bootloaders tend to be slower but have a baud rate quantisation error of less than 0.5%;
there are a number of bootloaders on offer in steps of 1.25% around the nominal F<sub>CPU</sub> so
that a particular board can be furnished with a suitable bootloader for the *actual* internal clock
frequency. All in all the aim is to ensure baud rate errors are below 2.5% to facilitate reliable
serial communication.

The pre-compiled `.hex` bootloaders of the
[`boards`](https://github.com/stefanrueger/urboot.hex/tree/main/boards/) and
[`cores`](https://github.com/stefanrueger/urboot.hex/tree/main/cores/) directories are copies of
selected relevant bootloaders in the
[`mcus`](https://github.com/stefanrueger/urboot.hex/tree/main/mcus/) tree, typically engaging the
correct activity LED for visual feedback while the bootloader is active. With these bootloaders the
board LED comes on after an external reset of the board at the beginning of each character read
`getch()` routine and is switched off at the end of each `getch()`. When the bootloader times out
at the end of its engagement the LED is switched off (unless, of course, it is used thereafter in
the uploaded application). There is no need to select a bootloader with
[blinkenlights](https://en.wikipedia.org/wiki/Blinkenlights): a silent bootloader from the
corresponding [`mcus`](https://github.com/stefanrueger/urboot.hex/tree/main/mcus/) tree which has
`_no-led` in the filename would equally be suitable for the board/core in consideration.

All in all, this repository contains 1,119,102 *different* current `u8.0` bootloaders amongst the
8,044,668 bootloader files on offer in the
[`mcus`](https://github.com/stefanrueger/urboot.hex/tree/main/mcus/) tree (4,611,934), the
[`boards`](https://github.com/stefanrueger/urboot.hex/tree/main/boards/) tree (1,080,684) and the
[`cores`](https://github.com/stefanrueger/urboot.hex/tree/main/cores/) tree (2,352,050). One reason
why some bootloaders are copies of each other is because, eg, a bootloader on 115,200 baud for 16
MHz is *exactly* the same as a bootloader on 57,600 baud for 8 MHz. The copies under different
names and boards/cores directories are provided for convenience.

The 1,283,806 *different* bootloaders of the previous version in the
[`u7.7`](https://github.com/stefanrueger/urboot.hex/tree/main/u7.7/) directory tree are less
interesting as they are usually bigger for the same features; none of them has the update feature
introduced in `u8.0`. The `u7.7` directory contains, however, a number of now deprecated `s`-type
bootloaders that follow a skeleton STK500v1 protocol; these bootloaders can be used with `avrdude
-c arduino` and older avrdude versions instead of the `avrdude -c urclock` programmer that urboot
bootloaders otherwise require.

Click on the links below to get more information about
 - The [urboot](https://github.com/stefanrueger/urboot/) project
 - Its [background](https://github.com/stefanrueger/urboot/blob/main/docs/background.md)
 - [Compiling](https://github.com/stefanrueger/urboot/blob/main/README.md#compiling) your own bootloader using urboot [make options](https://github.com/stefanrueger/urboot/blob/main/docs/makeoptions.md)
 - [Selecting](https://github.com/stefanrueger/urboot/blob/main/docs/howtoselect.md) the right bootloader for you
 - [Using](https://github.com/stefanrueger/urboot/blob/main/README.md#usage) them
 - How they [compare](https://github.com/stefanrueger/urboot/blob/main/README.md#comparison) to optiboot
 - And, finally, how to [trouble-shoot](https://github.com/stefanrueger/urboot/blob/main/README.md#trouble-shooting) them if things go wrong

Cloning this repository can take long and create a large directory (some 120 GB). Pro tip: Download a zip file instead from github or execute on the command line
```
curl -L https://github.com/stefanrueger/urboot.hex/tarball/master >urboot-hex.tar
```
This creates 3.4 GB gzip compressed tar file from the current snapshot.
