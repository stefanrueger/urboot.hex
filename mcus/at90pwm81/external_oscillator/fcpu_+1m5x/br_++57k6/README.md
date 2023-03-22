The AT90PWM81 exhibits a SWIO baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-hpr--`|[urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_lednop_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm81/external_oscillator/fcpu_+1m5x/br_++57k6/urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_lednop_hw.hex)|
|316|320|u7.7|`w-u-jPr-c`|[urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm81/external_oscillator/fcpu_+1m5x/br_++57k6/urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_lednop_fr_ce.hex)|
|320|320|u7.7|`weu-jpr--`|[urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm81/external_oscillator/fcpu_+1m5x/br_++57k6/urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop.hex)|
|378|384|u7.7|`weu-jPr-c`|[urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop_fr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm81/external_oscillator/fcpu_+1m5x/br_++57k6/urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop_fr_ce.hex)|
|360|512|u7.7|`weu-hpr-c`|[urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop_fr_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm81/external_oscillator/fcpu_+1m5x/br_++57k6/urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop_fr_ce_hw.hex)|
|464|512|u7.7|`wes-hpr-c`|[urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop_fr_ce_stk500_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm81/external_oscillator/fcpu_+1m5x/br_++57k6/urboot_at90pwm81_+1m5x_++57k6_swio_rxb0_txb1_ee_lednop_fr_ce_stk500_hw.hex)|

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
  + `12m0x` is F<sub>CPU</sub> of an external oscillator, here 12.0 MHz
  + `115k2` shows the fixed baud rate of the bootloader: `115k2` means 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `ee` bootloader supports EEPROM read/write
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `fr` bootloader provides non-essential code ("frills") for smoother error handling
  + `ce` bootloader provides a chip erase command
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to reset vector
