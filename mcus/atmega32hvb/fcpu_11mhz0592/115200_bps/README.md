|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jpr--`|[urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_lednop_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32hvb/fcpu_11mhz0592/115200_bps/urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_lednop_ur_vbl.hex)|
|376|384|u7.7|`weu-jPr-c`|[urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_ee_lednop_fr_ce_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32hvb/fcpu_11mhz0592/115200_bps/urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_ee_lednop_fr_ce_ur_vbl.hex)|
|358|512|u7.7|`weu-hpr-c`|[urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_ee_lednop_fr_ce_ur.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32hvb/fcpu_11mhz0592/115200_bps/urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_ee_lednop_fr_ce_ur.hex)|
|462|512|u7.7|`wes-hpr-c`|[urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32hvb/fcpu_11mhz0592/115200_bps/urboot_atmega32hvb_11mhz0592_115200bps_swio_rxb0_txb1_ee_lednop_fr_ce.hex)|

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
- **Hex file:** typically MCU name, oscillator frequency (16 MHz default) and baud rate (115200 default) followed by
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code for smoother error handing
  + `ce` bootloader provides a chip erase command
  + `ur` uses urprotocol and requires `avrdude -c urclock` for programming
  + `vbl` vector bootloader: set fuses to jump to reset, not the HW boot section
