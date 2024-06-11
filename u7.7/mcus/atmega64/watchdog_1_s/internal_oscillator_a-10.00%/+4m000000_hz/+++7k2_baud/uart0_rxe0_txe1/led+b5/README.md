The ATmega64 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|292|512|u7.7|`w-u-jPr--`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5.hex)|
|292|512|u7.7|`w-u-jPr--`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5_pr.hex)|
|316|512|u7.7|`w-u-jPr-c`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5_pr_ce.hex)|
|352|512|u7.7|`weu-jPr--`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5_pr_ee.hex)|
|376|512|u7.7|`weu-jPr-c`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5_pr_ee_ce.hex)|
|362|1024|u7.7|`weu-hpr-c`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5_ee_ce_hw.hex)|
|466|1024|u7.7|`wes-hpr-c`|[urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led+b5_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64/watchdog_1_s/internal_oscillator_a-10.00%25/%2B4m000000_hz/%2B%2B%2B7k2_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m64_1s_a4m0_7k2_swio_rxe0_txe1_led%2Bb5_ee_ce_hw_stk500.hex)|

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
  + `a4m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 4.0 MHz - 10.00%
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `swio` software I/O (not UART)
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
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr_ce
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr_ee
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr_ee_ce
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_ee_ce_hw
make MCU=atmega64 WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=234 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=220 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf79 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=196 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf8b -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=160 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf97 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=136 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce97 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=662 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xcecb -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=558 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64_1s_a8m0_14k4_swio_rxe0_txe1_led+b5_ee_ce_hw_stk500.elf urboot.c
```

