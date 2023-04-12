The ATmega64A exhibits a SWIO baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|292|512|u7.7|`w-u-jPr--`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop.hex)|
|292|512|u7.7|`w-u-jPr--`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr.hex)|
|316|512|u7.7|`w-u-jPr-c`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr_ce.hex)|
|352|512|u7.7|`weu-jPr--`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr_ee.hex)|
|376|512|u7.7|`weu-jPr-c`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_pr_ee_ce.hex)|
|362|1024|u7.7|`weu-hpr-c`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_ee_ce_hw.hex)|
|466|1024|u7.7|`wes-hpr-c`|[urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64a/watchdog_2_s/internal_oscillator_d-6.25%25/%2B4m000000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/lednop/urboot_m64a_2s_d4m0_14k4_swio_rxd2_txd3_lednop_ee_ce_hw_stk500.hex)|

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
  + `d4m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 4.0 MHz - 6.25%
  + `14k4` shows the fixed communication baud rate, here 14400 baud
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
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr_ce
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr_ee
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr_ee_ce
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_ee_ce_hw
make MCU=atmega64a WDTO=2S F_CPU=7500000L BAUD_RATE=28800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf64 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=252 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf64 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=238 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf70 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=214 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf82 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=178 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf8e -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=154 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce8e -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=680 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xcec1 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=578 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64a -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64a_2s_d8m0_28k8_swio_rxd2_txd3_lednop_ee_ce_hw_stk500.elf urboot.c
```

