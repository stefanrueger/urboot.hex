The ATmega328P @ 24000000 Hz has a UART baud rate of 250000 baud = 250000+0.00% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_fr.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_fr_ce.hex)|
|382|384|u7.7|`w-udjPr--`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_csb0_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_csb0_dual.hex)|
|330|512|u7.7|`weu-hpr-c`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_fr_ce_hw.hex)|
|382|512|u7.7|`w-udjpr--`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_csb0_dual_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_csb0_dual_fr.hex)|
|434|512|u7.7|`wes-hpr-c`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_fr_ce_stk500_hw.hex)|
|474|512|u7.7|`weudhpr-c`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_csb0_dual_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_csb0_dual_fr_ce_hw.hex)|
|482|512|u7.7|`w-sdhpr--`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_csb0_dual_fr_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_led-b1_csb0_dual_fr_stk500_hw.hex)|
|578|1024|u7.7|`wesdhpr-c`|[urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_csb0_dual_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclock/external_oscillator/fcpu++5m5296_Hz/br+++57k6_bps/urboot+urclock++5m5296x+++57k6_uart0_rxd0_txd1_ee_led-b1_csb0_dual_fr_ce_stk500_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `d` dual boot (over-the-air programming from external SPI flash)
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
  + `csb0` for dual boot uses, in this example, pin B0 as chip select of external SPI flash memory
  + `dual` boot both from external SPI flash memory and from serial interface
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to reset vector
