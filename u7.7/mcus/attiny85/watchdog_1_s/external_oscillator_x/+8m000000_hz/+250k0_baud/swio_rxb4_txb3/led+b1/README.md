The ATtiny85 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jpr--`|[urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led+b1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led%2Bb1.hex)|
|284|320|u7.7|`w-u-jPr--`|[urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led+b1_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led%2Bb1_pr.hex)|
|310|320|u7.7|`w-u-jPr-c`|[urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led+b1_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led%2Bb1_pr_ce.hex)|
|352|384|u7.7|`weu-jPr--`|[urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led+b1_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led%2Bb1_pr_ee.hex)|
|378|384|u7.7|`weu-jPr-c`|[urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led+b1_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_1s_x8m0_250k0_swio_rxb4_txb3_led%2Bb1_pr_ee_ce.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x8m0` is F<sub>CPU</sub> of an external oscillator, here 8.0 MHz
  + `250k0` shows the fixed communication baud rate, here 250000 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b1` toggles an active-high (`+`) LED on pin `B1`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny85 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1
make MCU=attiny85 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr
make MCU=attiny85 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr_ce
make MCU=attiny85 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr_ee
make MCU=attiny85 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_1s_x18m432_576k0_swio_rxb4_txb3_led+b1_pr_ee_ce.elf urboot.c
```

