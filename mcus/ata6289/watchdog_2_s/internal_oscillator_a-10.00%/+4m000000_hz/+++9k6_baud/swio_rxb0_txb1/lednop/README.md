The ATA6289 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---hpr--`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_hw.hex)|
|256|256|u8.0|`w---jpr--`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop.hex)|
|318|320|u8.0|`w---jPr-c`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ce.hex)|
|318|320|u8.0|`w-U-jPr--`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr.hex)|
|370|384|u8.0|`we--jPr-c`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|
|380|384|u8.0|`weU-jPr--`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee.hex)|
|418|512|u8.0|`weU-hpr-c`|[urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6289/watchdog_2_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/lednop/urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_ee_ce_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `a4m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 4.0 MHz - 10.00%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_hw
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ce
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee_ce
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee
make MCU=ata6289 WDTO=2S F_CPU=3600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd3 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf9d -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6289 -DF_CPU=3600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6289_2s_a4m0_9k6_swio_rxb0_txb1_lednop_ee_ce_hw.elf urboot.c
```

