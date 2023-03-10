|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|240|256|u7.7|`w-u-jPr--`|[urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_led+b5_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/fcpu_24mhz/500000_bps/urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_led+b5_ur_vbl.hex)|
|244|256|u7.7|`w-u-jpr--`|[urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_led+b5_fr_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/fcpu_24mhz/500000_bps/urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_led+b5_fr_ur_vbl.hex)|
|288|320|u7.7|`w-u-jPr-c`|[urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_led+b5_fr_ce_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/fcpu_24mhz/500000_bps/urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_led+b5_fr_ce_ur_vbl.hex)|
|320|320|u7.7|`weu-jPr--`|[urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_ee_led+b5_fr_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/fcpu_24mhz/500000_bps/urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_ee_led+b5_fr_ur_vbl.hex)|
|346|384|u7.7|`weu-jPr-c`|[urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_ee_led+b5_fr_ce_ur_vbl.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/fcpu_24mhz/500000_bps/urboot_atmega48p_24mhz_500000bps_uart0_rxd0_txd1_ee_led+b5_fr_ce_ur_vbl.hex)|

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
- **Hex file:** typically MCU name, oscillator frequency (16 MHz default) and baud rate (115200 default) followed by
  + `uart0` UART number, in this case `0`
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `led-b1` toggles an active-low LED on pin `B1`, `+` designates an active-high LED
  + `fr` bootloader provides non-essential code for smoother error handing
  + `ce` bootloader provides a chip erase command
  + `ur` uses urprotocol and requires `avrdude -c urclock` for programming
  + `vbl` vector bootloader: set fuses to jump to reset, not the HW boot section
