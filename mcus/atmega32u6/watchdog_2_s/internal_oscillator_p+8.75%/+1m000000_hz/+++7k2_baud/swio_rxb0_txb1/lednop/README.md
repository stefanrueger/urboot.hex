The ATmega32U6 exhibits a SWIO baud rate quantisation error of +0.03% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.03% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop.hex)|
|286|384|u7.7|`w-u-jPr--`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr.hex)|
|312|384|u7.7|`w-u-jPr-c`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr_ce.hex)|
|348|384|u7.7|`weu-jPr--`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr_ee.hex)|
|374|384|u7.7|`weu-jPr-c`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|
|356|512|u7.7|`weu-hpr-c`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_ee_ce_hw.hex)|
|460|512|u7.7|`wes-hpr-c`|[urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32u6/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/lednop/urboot_m32u6_2s_p1m0_7k2_swio_rxb0_txb1_lednop_ee_ce_hw_stk500.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `p1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 7%
  + `7k2` shows the fixed communication baud rate, here 7200 baud
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
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr_ce
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr_ee
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr_ee_ce
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_ee_ce_hw
make MCU=atmega32u6 WDTO=2S F_CPU=8700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa0 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=116 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=90 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8c -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=174 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=72 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32u6 -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32u6_2s_p8m0_57k6_swio_rxb0_txb1_lednop_ee_ce_hw_stk500.elf urboot.c
```

