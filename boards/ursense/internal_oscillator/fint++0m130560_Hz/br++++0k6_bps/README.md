The ATmega328P @ 130560 Hz has a SWIO baud rate of 598 baud = 600-0.33% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jpr--`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_led-d5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_led-d5.hex)|
|376|384|u7.7|`weu-jPr-c`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_fr_ce.hex)|
|358|512|u7.7|`weu-hpr-c`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_fr_ce_hw.hex)|
|450|512|u7.7|`w-udjPr-c`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_led-d5_csb0_dual_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_led-d5_csb0_dual_fr_ce.hex)|
|462|512|u7.7|`wes-hpr-c`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_fr_ce_stk500_hw.hex)|
|490|512|u7.7|`weudjPr--`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_csb0_dual_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_csb0_dual_fr.hex)|
|502|512|u7.7|`weudhpr-c`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_csb0_dual_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_csb0_dual_fr_ce_hw.hex)|
|510|512|u7.7|`w-sdhpr--`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_led-d5_csb0_dual_fr_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_led-d5_csb0_dual_fr_stk500_hw.hex)|
|606|1024|u7.7|`wesdhpr-c`|[urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_csb0_dual_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/internal_oscillator/fint++0m130560_Hz/br++++0k6_bps/urboot+ursense++0m130560i++++0k6_swio_rxd0_txd1_ee_led-d5_csb0_dual_fr_ce_stk500_hw.hex)|

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
  + `9m6000i` is F<sub>CPU</sub> of an internal oscillator, here 9.6000 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `led-b1` toggles an active-low LED on pin `B1`, `+` designates an active-high LED
  + `csb0` for dual boot uses, in this example, pin B0 as chip select of external SPI flash memory
  + `dual` boot both from external SPI flash memory and from serial interface
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to reset vector
