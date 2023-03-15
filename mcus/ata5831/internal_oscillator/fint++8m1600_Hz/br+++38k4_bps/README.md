The ATA5831 @ 8160000 Hz has a SWIO baud rate of 38309 baud = 38400-0.24% baud.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_lednop.hex)|
|304|320|u7.7|`w-u-jPr-c`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_lednop_fr_ce.hex)|
|316|320|u7.7|`weu-jpr--`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee.hex)|
|322|384|u7.7|`weu-jpr--`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop.hex)|
|366|384|u7.7|`weu-jPr-c`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop_fr_ce.hex)|
|346|20464|u7.7|`weu-hpr-c`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop_fr_ce_hw.hex)|
|450|20464|u7.7|`wes-hpr-c`|[urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/internal_oscillator/fint++8m1600_Hz/br+++38k4_bps/urboot+ata5831++8m1600i+++38k4_swio_rxb0_txb1_ee_lednop_fr_ce_stk500_hw.hex)|

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
- **Hex file:** typically MCU name followed by
  + `9m6000i` is F<sub>CPU</sub> of an internal oscillator, here 9.6000 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to reset vector
