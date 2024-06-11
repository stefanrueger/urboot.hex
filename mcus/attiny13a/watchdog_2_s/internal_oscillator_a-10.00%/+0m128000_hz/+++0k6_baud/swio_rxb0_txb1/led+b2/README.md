The ATtiny13A exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jPr--`|[urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_2_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led%2Bb2.hex)|
|254|256|u8.0|`w---jPr--`|[urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_2_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led%2Bb2_pr.hex)|
|288|288|u8.0|`w---jPr-c`|[urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_2_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led%2Bb2_pr_ce.hex)|
|316|320|u8.0|`we--jPr--`|[urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_2_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led%2Bb2_pr_ee.hex)|
|346|352|u8.0|`we--jPr-c`|[urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_2_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/swio_rxb0_txb1/led%2Bb2/urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led%2Bb2_pr_ee_ce.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `a0m128` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.128 MHz - 10.00%
  + `0k6` shows the fixed communication baud rate, here 600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b2` toggles an active-high (`+`) LED on pin `B2`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13a WDTO=2S F_CPU=115200L BAUD_RATE=600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2
make MCU=attiny13a WDTO=2S F_CPU=115200L BAUD_RATE=600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr
make MCU=attiny13a WDTO=2S F_CPU=115200L BAUD_RATE=600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ce
make MCU=attiny13a WDTO=2S F_CPU=115200L BAUD_RATE=600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ee
make MCU=attiny13a WDTO=2S F_CPU=115200L BAUD_RATE=600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB2 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=115200L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=115200L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=115200L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2c0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x2c0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=115200L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=115200L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB2 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_2s_a0m128_0k6_swio_rxb0_txb1_led+b2_pr_ee_ce.elf urboot.c
```

