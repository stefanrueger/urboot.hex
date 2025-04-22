The ATtiny13 exhibits a SWIO baud rate quantisation error of -0.15% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.15% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_attiny13.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13/watchdog_2_s/internal_oscillator/9480000_hz/9600_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_attiny13_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13/watchdog_2_s/internal_oscillator/9480000_hz/9600_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13_pr.hex)|
|286|288|u8.0|`w---jPr-c`|[urboot_attiny13_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13/watchdog_2_s/internal_oscillator/9480000_hz/9600_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13_pr_ce.hex)|
|314|320|u8.0|`we--jPr--`|[urboot_attiny13_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13/watchdog_2_s/internal_oscillator/9480000_hz/9600_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13_pr_ee.hex)|
|352|352|u8.0|`we--jPr-c`|[urboot_attiny13_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13/watchdog_2_s/internal_oscillator/9480000_hz/9600_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13_pr_ee_ce.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13 WDTO=2S F_CPU=9480000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2
make MCU=attiny13 WDTO=2S F_CPU=9480000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr
make MCU=attiny13 WDTO=2S F_CPU=9480000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr_ce
make MCU=attiny13 WDTO=2S F_CPU=9480000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr_ee
make MCU=attiny13 WDTO=2S F_CPU=9480000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9480000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9480000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9480000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2c0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x2c0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9480000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=5 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=9480000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_h9m6_9k6_swio_rxb1_txb0_led+b2_pr_ee_ce.elf urboot.c
```

