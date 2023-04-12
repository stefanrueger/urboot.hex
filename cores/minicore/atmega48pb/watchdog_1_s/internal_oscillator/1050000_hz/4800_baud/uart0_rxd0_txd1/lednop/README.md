The ATmega48PB exhibits a SWIO baud rate quantisation error of -0.11% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.11% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|296|320|u7.7|`w-u-jPr--`|[urboot_atmega48pb.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48pb/watchdog_1_s/internal_oscillator/1050000_hz/4800_baud/uart0_rxd0_txd1/lednop/urboot_atmega48pb.hex)|
|296|320|u7.7|`w-u-jPr--`|[urboot_atmega48pb_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48pb/watchdog_1_s/internal_oscillator/1050000_hz/4800_baud/uart0_rxd0_txd1/lednop/urboot_atmega48pb_pr.hex)|
|314|320|u7.7|`w-u-jPr-c`|[urboot_atmega48pb_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48pb/watchdog_1_s/internal_oscillator/1050000_hz/4800_baud/uart0_rxd0_txd1/lednop/urboot_atmega48pb_pr_ce.hex)|
|354|384|u7.7|`weu-jPr--`|[urboot_atmega48pb_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48pb/watchdog_1_s/internal_oscillator/1050000_hz/4800_baud/uart0_rxd0_txd1/lednop/urboot_atmega48pb_pr_ee.hex)|
|380|384|u7.7|`weu-jPr-c`|[urboot_atmega48pb_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48pb/watchdog_1_s/internal_oscillator/1050000_hz/4800_baud/uart0_rxd0_txd1/lednop/urboot_atmega48pb_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega48pb WDTO=1S F_CPU=8400000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop
make MCU=atmega48pb WDTO=1S F_CPU=8400000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr
make MCU=atmega48pb WDTO=1S F_CPU=8400000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr_ce
make MCU=atmega48pb WDTO=1S F_CPU=8400000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr_ee
make MCU=atmega48pb WDTO=1S F_CPU=8400000L BAUD_RATE=38400 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=56 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=4 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfc2 -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=48 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfcf -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48pb_1s_m8m0_38k4_swio_rxd0_txd1_lednop_pr_ee_ce.elf urboot.c
```

