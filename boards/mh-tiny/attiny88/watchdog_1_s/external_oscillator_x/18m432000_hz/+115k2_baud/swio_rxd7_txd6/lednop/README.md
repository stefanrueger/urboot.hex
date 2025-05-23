The ATtiny88 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jpr--`|[urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/18m432000_hz/%2B115k2_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop.hex)|
|306|320|u8.0|`w---jPr-c`|[urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/18m432000_hz/%2B115k2_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr_ce.hex)|
|318|320|u8.0|`w-U-jPr--`|[urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/18m432000_hz/%2B115k2_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr.hex)|
|318|320|u8.0|`we--jPr--`|[urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/18m432000_hz/%2B115k2_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mh-tiny/attiny88/watchdog_1_s/external_oscillator_x/18m432000_hz/%2B115k2_baud/swio_rxd7_txd6/lednop/urboot_t88_1s_x18m432_115k2_swio_rxd7_txd6_lednop_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x18m432` is F<sub>CPU</sub> of an external oscillator, here 18.432 MHz
  + `115k2` shows the fixed communication baud rate, here 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr_ce
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr_ee
make MCU=attiny88 WDTO=1S F_CPU=20000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcf -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_1s_x20m0_125k0_swio_rxd7_txd6_lednop_pr_ee_ce.elf urboot.c
```

