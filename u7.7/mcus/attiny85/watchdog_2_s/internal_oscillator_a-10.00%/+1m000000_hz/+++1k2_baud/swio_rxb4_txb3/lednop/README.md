The ATtiny85 exhibits a SWIO baud rate quantisation error of +0.12% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.12% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_2_s/internal_oscillator_a-10.00%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb4_txb3/lednop/urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop.hex)|
|280|320|u7.7|`w-u-jPr--`|[urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_2_s/internal_oscillator_a-10.00%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb4_txb3/lednop/urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr.hex)|
|306|320|u7.7|`w-u-jPr-c`|[urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_2_s/internal_oscillator_a-10.00%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb4_txb3/lednop/urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr_ce.hex)|
|348|384|u7.7|`weu-jPr--`|[urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_2_s/internal_oscillator_a-10.00%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb4_txb3/lednop/urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr_ee.hex)|
|374|384|u7.7|`weu-jPr-c`|[urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny85/watchdog_2_s/internal_oscillator_a-10.00%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb4_txb3/lednop/urboot_t85_2s_a1m0_1k2_swio_rxb4_txb3_lednop_pr_ee_ce.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `a1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 10.00%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny85 WDTO=2S F_CPU=7200000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop
make MCU=attiny85 WDTO=2S F_CPU=7200000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr
make MCU=attiny85 WDTO=2S F_CPU=7200000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr_ce
make MCU=attiny85 WDTO=2S F_CPU=7200000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr_ee
make MCU=attiny85 WDTO=2S F_CPU=7200000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=40 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny85 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t85_2s_a8m0_9k6_swio_rxb4_txb3_lednop_pr_ee_ce.elf urboot.c
```

