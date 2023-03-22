The ATtiny2313A exhibits a SWIO baud rate quantisation error of -0.12% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.12% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_lednop.hex)|
|278|288|u7.7|`w-u-jPr--`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_lednop_fr.hex)|
|288|288|u7.7|`w-u-jpr-c`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_lednop_fr_ce.hex)|
|310|320|u7.7|`weu-jpr--`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee_lednop.hex)|
|318|320|u7.7|`weu-jPr--`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee.hex)|
|342|352|u7.7|`weu-jPr--`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee_lednop_fr.hex)|
|352|352|u7.7|`weu-jpr-c`|[urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313a/internal_oscillator/fcpu_+8m0h-1/br_++19k2/urboot_attiny2313a_+8m0h-1_++19k2_swio_rxd0_txd1_ee_lednop_fr_ce.hex)|

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
  + `8m0j+1` is F<sub>CPU</sub> of an internal oscillator varied by some percent, here 8 MHz + 1%
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
