|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|240|256|u7.7|`w-u-jPr--`|[urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_lednop_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb162/fcpu_7mhz3728/4800_bps/urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_lednop_ur_vbl.hex)|
|244|256|u7.7|`w-u-jpr--`|[urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_lednop_fr_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb162/fcpu_7mhz3728/4800_bps/urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_lednop_fr_ur_vbl.hex)|
|350|384|u7.7|`weu-jPr-c`|[urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_ee_lednop_fr_ce_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb162/fcpu_7mhz3728/4800_bps/urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_ee_lednop_fr_ce_ur_vbl.hex)|
|332|512|u7.7|`weu-hpr-c`|[urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_ee_lednop_fr_ce_ur.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb162/fcpu_7mhz3728/4800_bps/urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_ee_lednop_fr_ce_ur.hex)|
|436|512|u7.7|`wes-hpr-c`|[urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb162/fcpu_7mhz3728/4800_bps/urboot_at90usb162_7mhz3728_4800bps_uart0_rxd2_txd3_ee_lednop_fr_ce.hex)|

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
  + `uart0` UART number, in this case `0`
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code for smoother error handing
  + `ce` bootloader provides a chip erase command
  + `ur` uses urprotocol and requires `avrdude -c urclock` for programming
  + `vbl` vector bootloader: set fuses to jump to reset, not the HW boot section
