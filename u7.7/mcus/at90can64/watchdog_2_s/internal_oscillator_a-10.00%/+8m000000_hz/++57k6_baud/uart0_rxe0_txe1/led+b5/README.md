The AT90CAN64 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5.hex)|
|288|512|u7.7|`w-u-jPr--`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5_pr.hex)|
|312|512|u7.7|`w-u-jPr-c`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5_pr_ce.hex)|
|348|512|u7.7|`weu-jPr--`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5_pr_ee.hex)|
|372|512|u7.7|`weu-jPr-c`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5_pr_ee_ce.hex)|
|358|1024|u7.7|`weu-hpr-c`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5_ee_ce_hw.hex)|
|462|1024|u7.7|`wes-hpr-c`|[urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90can64/watchdog_2_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B57k6_baud/uart0_rxe0_txe1/led%2Bb5/urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led%2Bb5_ee_ce_hw_stk500.hex)|

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
  + `a8m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 8.0 MHz - 10.00%
  + `57k6` shows the fixed communication baud rate, here 57600 baud
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
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ce
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ee
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ee_ce
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_ee_ce_hw
make MCU=at90can64 WDTO=2S F_CPU=7200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=224 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf79 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=200 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf8b -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=164 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf97 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=140 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce97 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=666 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xcecb -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=562 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can64 -DF_CPU=7200000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c64_2s_a8m0_57k6_swio_rxe0_txe1_led+b5_ee_ce_hw_stk500.elf urboot.c
```

