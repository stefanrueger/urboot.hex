The ATtiny13 exhibits a SWIO baud rate quantisation error of +0.05% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.05% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jPr--`|[urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led+b2.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m600000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led%2Bb2.hex)|
|254|256|u8.0|`w---jPr--`|[urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led+b2_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m600000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led%2Bb2_pr.hex)|
|288|288|u8.0|`w---jPr-c`|[urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led+b2_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m600000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led%2Bb2_pr_ce.hex)|
|316|320|u8.0|`we--jPr--`|[urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led+b2_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m600000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led%2Bb2_pr_ee.hex)|
|346|352|u8.0|`we--jPr-c`|[urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led+b2_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m600000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_1s_f0m6_1k2_swio_rxb0_txb1_led%2Bb2_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `f0m6` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.6 MHz - 3.75%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b2` toggles an active-high (`+`) LED on pin `B2`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13 WDTO=1S F_CPU=9240000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2
make MCU=attiny13 WDTO=1S F_CPU=9240000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr
make MCU=attiny13 WDTO=1S F_CPU=9240000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr_ce
make MCU=attiny13 WDTO=1S F_CPU=9240000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr_ee
make MCU=attiny13 WDTO=1S F_CPU=9240000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9240000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9240000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9240000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2c0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x2c0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9240000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9240000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_f9m6_19k2_swio_rxb0_txb1_led+b2_pr_ee_ce.elf urboot.c
```

