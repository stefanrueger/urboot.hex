The ATmega1280 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7_pr.hex)|
|314|512|u7.7|`w-u-jPr-c`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7_pr_ce.hex)|
|332|512|u7.7|`weu-jPr--`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7_pr_ee.hex)|
|376|512|u7.7|`weu-jPr-c`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7_pr_ee_ce.hex)|
|358|1024|u7.7|`weu-hpr-c`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7_ee_ce_hw.hex)|
|464|1024|u7.7|`wes-hpr-c`|[urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led+b7_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega1280/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B38k4_baud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_x3m6864_38k4_uart1_rxd2_txd3_led%2Bb7_ee_ce_hw_stk500.hex)|

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
  + `x3m6864` is F<sub>CPU</sub> of an external oscillator, here 3.6864 MHz
  + `38k4` shows the fixed communication baud rate, here 38400 baud
  + `uart1` UART number
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
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr_ce
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr_ee
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr_ee_ce
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_ee_ce_hw
make MCU=atmega1280 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf74 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=198 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf7d -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=180 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf93 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=136 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce93 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=666 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcec8 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=560 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_x24m0_250k0_uart1_rxd2_txd3_led+b7_ee_ce_hw_stk500.elf urboot.c
```

