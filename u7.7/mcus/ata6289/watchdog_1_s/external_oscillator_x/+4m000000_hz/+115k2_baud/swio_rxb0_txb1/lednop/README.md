The ATA6289 exhibits a SWIO baud rate quantisation error of -0.79% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.79% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|294|320|u7.7|`w-u-jPr--`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop.hex)|
|294|320|u7.7|`w-u-jPr--`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr.hex)|
|320|320|u7.7|`w-u-jPr-c`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr_ce.hex)|
|356|384|u7.7|`weu-jPr--`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr_ee.hex)|
|382|384|u7.7|`weu-jPr-c`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|
|276|512|u7.7|`w-u-hpr--`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_hw.hex)|
|364|512|u7.7|`weu-hpr-c`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_ee_ce_hw.hex)|
|468|512|u7.7|`wes-hpr-c`|[urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata6289/watchdog_1_s/external_oscillator_x/%2B4m000000_hz/%2B115k2_baud/swio_rxb0_txb1/lednop/urboot_a6289_1s_x4m0_115k2_swio_rxb0_txb1_lednop_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x4m0` is F<sub>CPU</sub> of an external oscillator, here 4.0 MHz
  + `115k2` shows the fixed communication baud rate, here 115200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr_ce
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr_ee
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr_ee_ce
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_hw
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_ee_ce_hw
make MCU=ata6289 WDTO=1S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=40 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=236 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf99 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=148 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=44 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_1s_x20m0_576k0_swio_rxb0_txb1_lednop_ee_ce_hw_stk500.elf urboot.c
```

