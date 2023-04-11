The ATtiny13 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B9m600000_hz/%2B%2B14k4_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led%2Bb2.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B9m600000_hz/%2B%2B14k4_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led%2Bb2_pr.hex)|
|288|288|u7.7|`w-u-jPr-c`|[urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B9m600000_hz/%2B%2B14k4_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led%2Bb2_pr_ce.hex)|
|342|352|u7.7|`weu-jPr--`|[urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B9m600000_hz/%2B%2B14k4_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led%2Bb2_pr_ee.hex)|
|352|352|u7.7|`weu-jPr-c`|[urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B9m600000_hz/%2B%2B14k4_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led%2Bb2_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `p9m6` is F<sub>CPU</sub> of a too fast internal oscillator, here 9.6 MHz + 8.75%
  + `14k4` shows the fixed communication baud rate, here 14400 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b2` toggles an active-high (`+`) LED on pin `B2`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13 WDTO=2S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2
make MCU=attiny13 WDTO=2S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr
make MCU=attiny13 WDTO=2S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ce
make MCU=attiny13 WDTO=2S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ee
make MCU=attiny13 WDTO=2S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=0 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=14400 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=14400 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=14400 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=14400 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=14400 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_p9m6_14k4_swio_rxb0_txb1_led+b2_pr_ee_ce.elf urboot.c
```

