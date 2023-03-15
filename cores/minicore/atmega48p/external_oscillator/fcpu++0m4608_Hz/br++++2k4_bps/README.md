The ATmega48P @ 24000000 Hz has a UART baud rate of 125000 baud = 125000+0.00% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_led+b5_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/external_oscillator/fcpu++0m4608_Hz/br++++2k4_bps/urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_led+b5_fr.hex)|
|286|320|u7.7|`w-u-jPr-c`|[urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_led+b5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/external_oscillator/fcpu++0m4608_Hz/br++++2k4_bps/urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_led+b5_fr_ce.hex)|
|318|320|u7.7|`weu-jPr--`|[urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_ee_led+b5_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/external_oscillator/fcpu++0m4608_Hz/br++++2k4_bps/urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_ee_led+b5_fr.hex)|
|344|384|u7.7|`weu-jPr-c`|[urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_ee_led+b5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/external_oscillator/fcpu++0m4608_Hz/br++++2k4_bps/urboot+atmega48p++0m4608x++++2k4_uart0_rxd0_txd1_ee_led+b5_fr_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** typically MCU name followed by
  + `12m0000x` is F<sub>CPU</sub> of an external oscillator, here 12.0000 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `uart0` UART number, in this case `0`
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `led-b1` toggles an active-low LED on pin `B1`, `+` designates an active-high LED
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
