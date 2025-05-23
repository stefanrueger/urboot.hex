The AT90CAN64 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jPr--`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5.hex)|
|252|256|u7.7|`w-u-jPr--`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5_pr.hex)|
|290|512|u7.7|`w-u-jPr-c`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5_pr_ce.hex)|
|326|512|u7.7|`weu-jPr--`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5_pr_ee.hex)|
|350|512|u7.7|`weu-jPr-c`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5_pr_ee_ce.hex)|
|336|1024|u7.7|`weu-hpr-c`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5_ee_ce_hw.hex)|
|440|1024|u7.7|`wes-hpr-c`|[urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led+b5_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_1_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_c64_1s_x2m304_57k6_uart1_rxd2_txd3_led%2Bb5_ee_ce_hw_stk500.hex)|

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
  + `x2m304` is F<sub>CPU</sub> of an external oscillator, here 2.304 MHz
  + `57k6` shows the fixed communication baud rate, here 57600 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr_ce
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr_ee
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr_ee_ce
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_ee_ce_hw
make MCU=at90can64 WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=3 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf6e -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=222 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf80 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=186 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf8c -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=162 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce8c -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=688 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xcec0 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=584 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_1s_x20m0_500k0_uart1_rxd2_txd3_led+b5_ee_ce_hw_stk500.elf urboot.c
```

