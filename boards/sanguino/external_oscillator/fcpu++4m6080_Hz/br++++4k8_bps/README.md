The ATmega644P @ 18432000 Hz has a UART baud rate of 19200 baud = 19200+0.00% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_led+b0_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_led+b0_fr.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_led+b0_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_led+b0_fr.hex)|
|340|512|u7.7|`weu-jPr-c`|[urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_ee_led+b0_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_ee_led+b0_fr_ce.hex)|
|340|512|u7.7|`weu-jPr-c`|[urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_ee_led+b0_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_ee_led+b0_fr_ce.hex)|
|326|1024|u7.7|`weu-hpr-c`|[urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_ee_led+b0_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_ee_led+b0_fr_ce_hw.hex)|
|326|1024|u7.7|`weu-hpr-c`|[urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_ee_led+b0_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_ee_led+b0_fr_ce_hw.hex)|
|430|1024|u7.7|`wes-hpr-c`|[urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_ee_led+b0_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart0_rxd0_txd1_ee_led+b0_fr_ce_stk500_hw.hex)|
|430|1024|u7.7|`wes-hpr-c`|[urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_ee_led+b0_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/sanguino/external_oscillator/fcpu++4m6080_Hz/br++++4k8_bps/urboot+sanguino++4m6080x++++4k8_uart1_rxd2_txd3_ee_led+b0_fr_ce_stk500_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
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
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to reset vector
