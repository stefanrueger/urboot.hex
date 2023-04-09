The ATA5702M322 exhibits a SWIO baud rate quantisation error of -0.22% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.22% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/external_oscillator/20m000000_hz/%2B230k4_baud/swio_rxb0_txb1/lednop/urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop.hex)|
|290|320|u7.7|`w-u-jPr--`|[urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/external_oscillator/20m000000_hz/%2B230k4_baud/swio_rxb0_txb1/lednop/urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr.hex)|
|316|320|u7.7|`w-u-jPr-c`|[urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/external_oscillator/20m000000_hz/%2B230k4_baud/swio_rxb0_txb1/lednop/urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ce.hex)|
|352|384|u7.7|`weu-jPr--`|[urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/external_oscillator/20m000000_hz/%2B230k4_baud/swio_rxb0_txb1/lednop/urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee.hex)|
|378|384|u7.7|`weu-jPr-c`|[urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/external_oscillator/20m000000_hz/%2B230k4_baud/swio_rxb0_txb1/lednop/urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|

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
  + `x20m0` is F<sub>CPU</sub> of an external oscillator, here 20.0 MHz
  + `a5702m322` is F<sub>CPU</sub> of a too slow internal oscillator, here 5702.322 MHz - 8%
  + `230k4` shows the fixed communication baud rate, here 230400 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5702m322 WDTO=1S F_CPU=20000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop
make MCU=ata5702m322 WDTO=1S F_CPU=20000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr
make MCU=ata5702m322 WDTO=1S F_CPU=20000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ce
make MCU=ata5702m322 WDTO=1S F_CPU=20000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee
make MCU=ata5702m322 WDTO=1S F_CPU=20000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=2 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7ec0UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x7ec0 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=48 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7ec0UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x7ec0 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc3 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=50 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_x20m0_230k4_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
```

