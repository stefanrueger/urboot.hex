The ATtiny88 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator/%2B0m921600_hz/%2B%2B%2B4k8_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop.hex)|
|282|320|u7.7|`w-u-jPr--`|[urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator/%2B0m921600_hz/%2B%2B%2B4k8_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr.hex)|
|308|320|u7.7|`w-u-jPr-c`|[urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator/%2B0m921600_hz/%2B%2B%2B4k8_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr_ce.hex)|
|322|384|u7.7|`weu-jPr--`|[urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator/%2B0m921600_hz/%2B%2B%2B4k8_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr_ee.hex)|
|366|384|u7.7|`weu-jPr-c`|[urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator/%2B0m921600_hz/%2B%2B%2B4k8_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x0m9216_4k8_swio_rxd7_txd6_lednop_pr_ee_ce.hex)|

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
  + `x0m9216` is F<sub>CPU</sub> of an external oscillator, here 0.9216 MHz
  + `4k8` shows the fixed communication baud rate, here 4800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny88 WDTO=1S F_CPU=24000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop
make MCU=attiny88 WDTO=1S F_CPU=24000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr
make MCU=attiny88 WDTO=1S F_CPU=24000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr_ce
make MCU=attiny88 WDTO=1S F_CPU=24000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr_ee
make MCU=attiny88 WDTO=1S F_CPU=24000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc0 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=56 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfbd -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x24m0_125k0_swio_rxd7_txd6_lednop_pr_ee_ce.elf urboot.c
```

