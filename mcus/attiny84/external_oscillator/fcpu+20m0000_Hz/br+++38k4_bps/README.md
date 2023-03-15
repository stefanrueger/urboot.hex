The ATtiny84 @ 20000000 Hz has a SWIO baud rate of 38387 baud = 38400-0.03% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_led+a4.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_led+a4.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_lednop.hex)|
|302|320|u7.7|`w-u-jPr-c`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_led+a4_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_led+a4_fr_ce.hex)|
|302|320|u7.7|`w-u-jPr-c`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_lednop_fr_ce.hex)|
|312|320|u7.7|`weu-jpr--`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_led+a4.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_led+a4.hex)|
|312|320|u7.7|`weu-jpr--`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_lednop.hex)|
|320|320|u7.7|`weu-jPr--`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee.hex)|
|370|384|u7.7|`weu-jPr-c`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_led+a4_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_led+a4_fr_ce.hex)|
|370|384|u7.7|`weu-jPr-c`|[urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/external_oscillator/fcpu+20m0000_Hz/br+++38k4_bps/urboot+attiny84+20m0000x+++38k4_swio_rxa3_txa2_ee_lednop_fr_ce.hex)|

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
- **Hex file:** typically MCU name followed by
  + `12m0000x` is F<sub>CPU</sub> of an external oscillator, here 12.0000 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `led-b1` toggles an active-low LED on pin `B1`, `+` designates an active-high LED
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
