The ATmega162 exhibits a UART baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|236|256|u7.7|`w-u-hpr--`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_hw.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_pr.hex)|
|280|384|u7.7|`w-u-jPr-c`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_pr_ce.hex)|
|314|384|u7.7|`weu-jPr--`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_pr_ee.hex)|
|340|384|u7.7|`weu-jPr-c`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_pr_ee_ce.hex)|
|322|512|u7.7|`weu-hpr-c`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_ee_ce_hw.hex)|
|426|512|u7.7|`wes-hpr-c`|[urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led+b0_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_1_s/external_oscillator/%2B0m500000_hz/%2B%2B%2B4k8_baud/uart1_rxb2_txb3/led%2Bb0/urboot_m162_1s_x0m5_4k8_uart1_rxb2_txb3_led%2Bb0_ee_ce_hw_stk500.hex)|

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
  + `x0m5` is F<sub>CPU</sub> of an external oscillator, here 0.5 MHz
  + `4k8` shows the fixed communication baud rate, here 4800 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b0` toggles an active-high (`+`) LED on pin `B0`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_hw
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr_ce
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr_ee
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr_ee_ce
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_ee_ce_hw
make MCU=atmega162 WDTO=1S F_CPU=24000000L BAUD_RATE=230400 UARTNUM=1 RX=AtmelPB2 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_hw.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcf9d -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=122 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfae -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=88 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=62 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf7b -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=208 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcfae -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=106 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=230400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_1s_x24m0_230k4_uart1_rxb2_txb3_led+b0_ee_ce_hw_stk500.elf urboot.c
```

