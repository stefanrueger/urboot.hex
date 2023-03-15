The ATmega48 @ 16000000 Hz has a UART baud rate of 1000000 baud = 1000000+0.00% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jPr--`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_led+b5_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_led+b5_fr.hex)|
|252|256|u7.7|`w-u-jPr--`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_lednop_fr.hex)|
|282|320|u7.7|`w-u-jPr-c`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_led+b5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_led+b5_fr_ce.hex)|
|282|320|u7.7|`w-u-jPr-c`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_lednop_fr_ce.hex)|
|318|320|u7.7|`weu-jPr--`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_led+b5_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_led+b5_fr.hex)|
|318|320|u7.7|`weu-jPr--`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_lednop_fr.hex)|
|344|384|u7.7|`weu-jPr-c`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_led+b5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_led+b5_fr_ce.hex)|
|344|384|u7.7|`weu-jPr-c`|[urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/external_oscillator/fcpu+14m7456_Hz/br++921k6_bps/urboot+atmega48+14m7456x++921k6_uart0_rxd0_txd1_ee_lednop_fr_ce.hex)|

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
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
