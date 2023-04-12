The ATtiny13A exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_attiny13a.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13a/watchdog_2_s/internal_oscillator/5040000_hz/28800_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13a.hex)|
|282|288|u7.7|`w-u-jPr--`|[urboot_attiny13a_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13a/watchdog_2_s/internal_oscillator/5040000_hz/28800_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13a_pr.hex)|
|288|288|u7.7|`w-u-jPr-c`|[urboot_attiny13a_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13a/watchdog_2_s/internal_oscillator/5040000_hz/28800_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13a_pr_ce.hex)|
|346|352|u7.7|`weu-jPr--`|[urboot_attiny13a_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13a/watchdog_2_s/internal_oscillator/5040000_hz/28800_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13a_pr_ee.hex)|
|352|352|u7.7|`weu-jPr-c`|[urboot_attiny13a_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/microcore/attiny13a/watchdog_2_s/internal_oscillator/5040000_hz/28800_baud/swio_rxb1_txb0/led%2Bb2/urboot_attiny13a_pr_ee_ce.hex)|

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
- **Hex file:** often qualified by the MCU name and/or configuration
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13a WDTO=2S F_CPU=10080000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2
make MCU=attiny13a WDTO=2S F_CPU=10080000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr
make MCU=attiny13a WDTO=2S F_CPU=10080000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr_ce
make MCU=attiny13a WDTO=2S F_CPU=10080000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr_ee
make MCU=attiny13a WDTO=2S F_CPU=10080000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10080000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=6 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10080000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10080000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=6 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10080000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10080000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_m9m6_57k6_swio_rxb1_txb0_led+b2_pr_ee_ce.elf urboot.c
```

