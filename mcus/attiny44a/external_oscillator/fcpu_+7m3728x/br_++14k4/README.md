The ATtiny44A exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u7.7|`w-u-jpr--`|[urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny44a/external_oscillator/fcpu_+7m3728x/br_++14k4/urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_lednop.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny44a/external_oscillator/fcpu_+7m3728x/br_++14k4/urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1.hex)|
|308|320|u7.7|`w-u-jPr-c`|[urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny44a/external_oscillator/fcpu_+7m3728x/br_++14k4/urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_lednop_fr_ce.hex)|
|318|320|u7.7|`weu-jpr--`|[urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny44a/external_oscillator/fcpu_+7m3728x/br_++14k4/urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_ee_lednop.hex)|
|376|384|u7.7|`weu-jPr-c`|[urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny44a/external_oscillator/fcpu_+7m3728x/br_++14k4/urboot_attiny44a_+7m3728x_++14k4_swio_rxb0_txb1_ee_lednop_fr_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** typically MCU name followed by, eg, F<sub>CPU</sub>, baud rate, I/O channels etc configuration
  + `12m0x` is F<sub>CPU</sub> of an external oscillator, here 12.0 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
