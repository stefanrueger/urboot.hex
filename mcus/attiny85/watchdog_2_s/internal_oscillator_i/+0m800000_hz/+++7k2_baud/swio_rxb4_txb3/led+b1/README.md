The ATtiny85 exhibits a SWIO baud rate quantisation error of +0.10% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.10% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jPr--`|[urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led+b1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny85/watchdog_2_s/internal_oscillator_i/%2B0m800000_hz/%2B%2B%2B7k2_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led%2Bb1.hex)|
|254|256|u8.0|`w---jPr--`|[urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led+b1_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny85/watchdog_2_s/internal_oscillator_i/%2B0m800000_hz/%2B%2B%2B7k2_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led%2Bb1_pr.hex)|
|300|320|u8.0|`w---jPr-c`|[urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led+b1_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny85/watchdog_2_s/internal_oscillator_i/%2B0m800000_hz/%2B%2B%2B7k2_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led%2Bb1_pr_ce.hex)|
|316|320|u8.0|`we--jPr--`|[urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led+b1_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny85/watchdog_2_s/internal_oscillator_i/%2B0m800000_hz/%2B%2B%2B7k2_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led%2Bb1_pr_ee.hex)|
|382|384|u8.0|`weU-jPr-c`|[urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led+b1_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny85/watchdog_2_s/internal_oscillator_i/%2B0m800000_hz/%2B%2B%2B7k2_baud/swio_rxb4_txb3/led%2Bb1/urboot_t85_2s_i0m8_7k2_swio_rxb4_txb3_led%2Bb1_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `i0m8` is F<sub>CPU</sub> of an internal oscillator, here 0.8 MHz
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b1` toggles an active-high (`+`) LED on pin `B1`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny85 WDTO=2S F_CPU=6400000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1
make MCU=attiny85 WDTO=2S F_CPU=6400000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr
make MCU=attiny85 WDTO=2S F_CPU=6400000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr_ce
make MCU=attiny85 WDTO=2S F_CPU=6400000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr_ee
make MCU=attiny85 WDTO=2S F_CPU=6400000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=6400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=6400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=6400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=6400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=6400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_i6m4_57k6_swio_rxb4_txb3_led+b1_pr_ee_ce.elf urboot.c
```

