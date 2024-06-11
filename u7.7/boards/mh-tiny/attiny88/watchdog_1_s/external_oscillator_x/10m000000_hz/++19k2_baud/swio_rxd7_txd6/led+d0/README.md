The ATtiny88 exhibits a SWIO baud rate quantisation error of -0.03% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.03% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led+d0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B19k2_baud/swio_rxd7_txd6/led%2Bd0/urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led%2Bd0.hex)|
|282|320|u7.7|`w-u-jPr--`|[urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led+d0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B19k2_baud/swio_rxd7_txd6/led%2Bd0/urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led%2Bd0_pr.hex)|
|308|320|u7.7|`w-u-jPr-c`|[urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led+d0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B19k2_baud/swio_rxd7_txd6/led%2Bd0/urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led%2Bd0_pr_ce.hex)|
|322|384|u7.7|`weu-jPr--`|[urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led+d0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B19k2_baud/swio_rxd7_txd6/led%2Bd0/urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led%2Bd0_pr_ee.hex)|
|366|384|u7.7|`weu-jPr-c`|[urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led+d0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B19k2_baud/swio_rxd7_txd6/led%2Bd0/urboot_t88_1s_x10m0_19k2_swio_rxd7_txd6_led%2Bd0_pr_ee_ce.hex)|

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
  + `x10m0` is F<sub>CPU</sub> of an external oscillator, here 10.0 MHz
  + `19k2` shows the fixed communication baud rate, here 19200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+d0` toggles an active-high (`+`) LED on pin `D0`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPD0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPD0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPD0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr_ce
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPD0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr_ee
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPD0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe5 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPD0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPD0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPD0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfbd -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPD0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd3 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPD0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_38k4_swio_rxd7_txd6_led+d0_pr_ee_ce.elf urboot.c
```

