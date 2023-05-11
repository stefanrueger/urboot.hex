The ATmega3290PA exhibits a SWIO baud rate quantisation error of +0.03% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.03% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|296|384|u7.7|`w-u-jPr--`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop.hex)|
|296|384|u7.7|`w-u-jPr--`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr.hex)|
|322|384|u7.7|`w-u-jPr-c`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr_ce.hex)|
|356|384|u7.7|`weu-jPr--`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr_ee.hex)|
|382|384|u7.7|`weu-jPr-c`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_pr_ee_ce.hex)|
|364|512|u7.7|`weu-hpr-c`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_ee_ce_hw.hex)|
|468|512|u7.7|`wes-hpr-c`|[urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega3290pa/watchdog_2_s/internal_oscillator_p%2B8.75%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart0_rxe0_txe1/lednop/urboot_m3290pa_2s_p1m0_2k4_swio_rxe0_txe1_lednop_ee_ce_hw_stk500.hex)|

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
  + `p1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 8.75%
  + `2k4` shows the fixed communication baud rate, here 2400 baud
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
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr_ce
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr_ee
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr_ee_ce
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_ee_ce_hw
make MCU=atmega3290pa WDTO=2S F_CPU=8700000L BAUD_RATE=19200 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfae -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=102 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfae -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=88 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=62 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf99 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=148 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=44 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290pa -DF_CPU=8700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290pa_2s_p8m0_19k2_swio_rxe0_txe1_lednop_ee_ce_hw_stk500.elf urboot.c
```

