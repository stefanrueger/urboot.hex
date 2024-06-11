The ATmega640 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7.hex)|
|284|512|u7.7|`w-u-jPr--`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7_pr.hex)|
|308|512|u7.7|`w-u-jPr-c`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7_pr_ce.hex)|
|346|512|u7.7|`weu-jPr--`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7_pr_ee.hex)|
|370|512|u7.7|`weu-jPr-c`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7_pr_ee_ce.hex)|
|356|1024|u7.7|`weu-hpr-c`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7_ee_ce_hw.hex)|
|460|1024|u7.7|`wes-hpr-c`|[urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega640/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led%2Bb7_ee_ce_hw_stk500.hex)|

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
  + `p0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 8.75%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b7` toggles an active-high (`+`) LED on pin `B7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ce
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ee
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ee_ce
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_ee_ce_hw
make MCU=atmega640 WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf6b -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=228 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf77 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=204 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf8a -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=166 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf96 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=142 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce96 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=668 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xceca -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=564 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_p0m128_1k2_swio_rxd2_txd3_led+b7_ee_ce_hw_stk500.elf urboot.c
```

