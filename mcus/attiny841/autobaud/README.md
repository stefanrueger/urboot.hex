Note that autobaud bootloaders normally can only detect host baud rates = f/8, f/16, ... f/2048 +/- 1.5%, where f=F<sub>CPU</sub>. Internal oscillators have a high unknown deviation: baud rates under f/260 are recommended for these.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|244|256|u7.7|`w-u-jpra-`|[urboot+attiny841+autobaud_uart0_rxa2_txa1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_rxa2_txa1_lednop.hex)|
|244|256|u7.7|`w-u-jpra-`|[urboot+attiny841+autobaud_uart1_rxa4_txa5_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart1_rxa4_txa5_lednop.hex)|
|250|256|u7.7|`w-u-jpra-`|[urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_lednop.hex)|
|252|256|u7.7|`w-u-jPra-`|[urboot+attiny841+autobaud_uart0_rxa2_txa1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_rxa2_txa1.hex)|
|252|256|u7.7|`w-u-jPra-`|[urboot+attiny841+autobaud_uart1_rxa4_txa5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart1_rxa4_txa5.hex)|
|306|320|u7.7|`w-u-jPrac`|[urboot+attiny841+autobaud_uart0_rxa2_txa1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_rxa2_txa1_lednop_fr_ce.hex)|
|306|320|u7.7|`w-u-jPrac`|[urboot+attiny841+autobaud_uart1_rxa4_txa5_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart1_rxa4_txa5_lednop_fr_ce.hex)|
|310|320|u7.7|`weu-jpra-`|[urboot+attiny841+autobaud_uart0_rxa2_txa1_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_rxa2_txa1_ee_lednop.hex)|
|310|320|u7.7|`weu-jpra-`|[urboot+attiny841+autobaud_uart1_rxa4_txa5_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart1_rxa4_txa5_ee_lednop.hex)|
|312|320|u7.7|`w-u-jPrac`|[urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_lednop_fr_ce.hex)|
|316|320|u7.7|`weu-jpra-`|[urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_ee_lednop.hex)|
|318|320|u7.7|`weu-jPra-`|[urboot+attiny841+autobaud_uart0_rxa2_txa1_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_rxa2_txa1_ee.hex)|
|318|320|u7.7|`weu-jPra-`|[urboot+attiny841+autobaud_uart1_rxa4_txa5_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart1_rxa4_txa5_ee.hex)|
|368|384|u7.7|`weu-jPrac`|[urboot+attiny841+autobaud_uart0_rxa2_txa1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_rxa2_txa1_ee_lednop_fr_ce.hex)|
|368|384|u7.7|`weu-jPrac`|[urboot+attiny841+autobaud_uart1_rxa4_txa5_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart1_rxa4_txa5_ee_lednop_fr_ce.hex)|
|374|384|u7.7|`weu-jPrac`|[urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/autobaud/urboot+attiny841+autobaud_uart0_alt1_rxb2_txa7_ee_lednop_fr_ce.hex)|

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
  + `a` autobaud detection (f_cpu/8n using discrete divisors, n = 1, 2, ..., 256)
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** typically MCU name followed by
  + `autobaud` detects host baud rate f/8, f/16, f/24, ..., f/2048 (f=F<sub>CPU</sub>)
  + `uart0` UART number, in this case `0`
  + `alt1` alternative RX/TX pin assignment
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
