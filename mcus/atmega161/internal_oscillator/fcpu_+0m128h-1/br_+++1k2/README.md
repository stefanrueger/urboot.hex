The ATmega161 exhibits a SWIO baud rate quantisation error of -0.42% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.42% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jpr--`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3.hex)|
|252|256|u7.7|`w-u-jpr--`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1.hex)|
|320|384|u7.7|`w-u-jPr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_lednop_fr_ce.hex)|
|320|384|u7.7|`w-u-jPr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_lednop_fr_ce.hex)|
|360|384|u7.7|`weu-jPr--`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr.hex)|
|360|384|u7.7|`weu-jPr--`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr.hex)|
|372|384|u7.7|`weu-jpr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr_ce.hex)|
|372|384|u7.7|`weu-jpr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr_ce.hex)|
|368|1024|u7.7|`weu-hpr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr_ce_hw.hex)|
|368|1024|u7.7|`weu-hpr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr_ce_hw.hex)|
|472|1024|u7.7|`wes-hpr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxb2_txb3_ee_lednop_fr_ce_stk500_hw.hex)|
|472|1024|u7.7|`wes-hpr-c`|[urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega161/internal_oscillator/fcpu_+0m128h-1/br_+++1k2/urboot_atmega161_+0m128h-1_+++1k2_swio_rxd0_txd1_ee_lednop_fr_ce_stk500_hw.hex)|

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
- **Hex file:** typically MCU name followed by, eg, F<sub>CPU</sub>, baud rate, I/O channels etc configuration
  + `8m0j+1` is F<sub>CPU</sub> of an internal oscillator varied by some percent, here 8 MHz + 1%
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to reset vector
