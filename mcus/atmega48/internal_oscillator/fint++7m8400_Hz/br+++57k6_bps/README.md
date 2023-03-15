The ATmega48 @ 7840000 Hz has a UART baud rate of 57647 baud = 57600+0.08% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_led+b5_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_led+b5_fr.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_lednop_fr.hex)|
|286|320|u7.7|`w-u-jPr-c`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_led+b5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_led+b5_fr_ce.hex)|
|286|320|u7.7|`w-u-jPr-c`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_lednop_fr_ce.hex)|
|304|320|u7.7|`weu-jPr--`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_led+b5.hex)|
|304|320|u7.7|`weu-jPr--`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_lednop.hex)|
|308|320|u7.7|`weu-jpr--`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_led+b5_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_led+b5_fr.hex)|
|308|320|u7.7|`weu-jpr--`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_lednop_fr.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_led+b5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_led+b5_fr_ce.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/internal_oscillator/fint++7m8400_Hz/br+++57k6_bps/urboot+atmega48++7m8400i+++57k6_uart0_rxd0_txd1_ee_lednop_fr_ce.hex)|

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
  + `9m6000i` is F<sub>CPU</sub> of an internal oscillator, here 9.6000 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `uart0` UART number, in this case `0`
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `led-b1` toggles an active-low LED on pin `B1`, `+` designates an active-high LED
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
