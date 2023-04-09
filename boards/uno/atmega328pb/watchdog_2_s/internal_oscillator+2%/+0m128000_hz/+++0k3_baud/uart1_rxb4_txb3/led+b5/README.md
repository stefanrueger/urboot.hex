The ATmega328PB exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5.hex)|
|286|384|u7.7|`w-u-jPr--`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5_pr.hex)|
|312|384|u7.7|`w-u-jPr-c`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5_pr_ce.hex)|
|348|384|u7.7|`weu-jPr--`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5_pr_ee.hex)|
|374|384|u7.7|`weu-jPr-c`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5_pr_ee_ce.hex)|
|356|512|u7.7|`weu-hpr-c`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5_ee_ce_hw.hex)|
|460|512|u7.7|`wes-hpr-c`|[urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_2_s/internal_oscillator%2B2%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led%2Bb5_ee_ce_hw_stk500.hex)|

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
  + `k0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 2%
  + `0k3` shows the fixed communication baud rate, here 300 baud
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
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ce
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ee
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ee_ce
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_ee_ce_hw
make MCU=atmega328pb WDTO=2S F_CPU=130560L BAUD_RATE=300 SWIO=1 RX=AtmelPB4 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa0 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=116 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=90 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8c -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=174 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=72 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=130560L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_2s_k0m128_0k3_swio_rxb4_txb3_led+b5_ee_ce_hw_stk500.elf urboot.c
```

