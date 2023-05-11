The ATmega168PB exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|296|384|u7.7|`w-u-jPr--`|[urboot_atmega168pb.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb.hex)|
|296|384|u7.7|`w-u-jPr--`|[urboot_atmega168pb_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_pr.hex)|
|322|384|u7.7|`w-u-jPr-c`|[urboot_atmega168pb_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_pr_ce.hex)|
|358|384|u7.7|`weu-jPr--`|[urboot_atmega168pb_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_pr_ee.hex)|
|384|384|u7.7|`weu-jPr-c`|[urboot_atmega168pb_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_pr_ee_ce.hex)|
|278|512|u7.7|`w-u-hpr--`|[urboot_atmega168pb_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_hw.hex)|
|366|512|u7.7|`weu-hpr-c`|[urboot_atmega168pb_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_ee_ce_hw.hex)|
|470|512|u7.7|`wes-hpr-c`|[urboot_atmega168pb_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega168pb/watchdog_1_s/internal_oscillator/137600_hz/600_baud/uart0_rxd0_txd1/lednop/urboot_atmega168pb_ee_ce_hw_stk500.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr_ce
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr_ee
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr_ee_ce
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_hw
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_ee_ce_hw
make MCU=atmega168pb WDTO=1S F_CPU=137600L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfae -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=102 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfae -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=88 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=62 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf6e -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=234 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf9a -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=146 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=137600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_o0m128_0k6_swio_rxd0_txd1_lednop_ee_ce_hw_stk500.elf urboot.c
```

