The ATmega328PB exhibits a SWIO baud rate quantisation error of +0.08% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.08% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_atmega328pb.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb.hex)|
|280|384|u7.7|`w-u-jPr--`|[urboot_atmega328pb_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb_pr.hex)|
|306|384|u7.7|`w-u-jPr-c`|[urboot_atmega328pb_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb_pr_ce.hex)|
|342|384|u7.7|`weu-jPr--`|[urboot_atmega328pb_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb_pr_ee.hex)|
|368|384|u7.7|`weu-jPr-c`|[urboot_atmega328pb_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb_pr_ee_ce.hex)|
|350|512|u7.7|`weu-hpr-c`|[urboot_atmega328pb_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb_ee_ce_hw.hex)|
|454|512|u7.7|`wes-hpr-c`|[urboot_atmega328pb_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega328pb/watchdog_1_s/internal_oscillator/950000_hz/1200_baud/uart0_rxd0_txd1/no-led/urboot_atmega328pb_ee_ce_hw_stk500.hex)|

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
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr_ce
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr_ee
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr_ee_ce
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_ee_ce_hw
make MCU=atmega328pb WDTO=1S F_CPU=7600000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe2 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa6 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb3 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=78 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf92 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=162 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_e8m0_9k6_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.elf urboot.c
```

