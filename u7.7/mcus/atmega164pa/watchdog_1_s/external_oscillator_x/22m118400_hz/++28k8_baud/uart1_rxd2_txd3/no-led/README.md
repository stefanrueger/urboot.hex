The ATmega164PA exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|236|256|u7.7|`w-u-hpr--`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_hw.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr.hex)|
|280|384|u7.7|`w-u-jPr-c`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ce.hex)|
|316|384|u7.7|`weu-jPr--`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee.hex)|
|342|384|u7.7|`weu-jPr-c`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee_ce.hex)|
|324|512|u7.7|`weu-hpr-c`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw.hex)|
|428|512|u7.7|`wes-hpr-c`|[urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega164pa/watchdog_1_s/external_oscillator_x/22m118400_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/no-led/urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw_stk500.hex)|

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
  + `x22m1184` is F<sub>CPU</sub> of an external oscillator, here 22.1184 MHz
  + `28k8` shows the fixed communication baud rate, here 28800 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_hw
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ce
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee_ce
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw
make MCU=atmega164pa WDTO=1S F_CPU=22118400L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_hw.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfa6 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb8 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=68 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf85 -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=188 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcfb9 -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=84 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164pa_1s_x22m1184_28k8_uart1_rxd2_txd3_no-led_ee_ce_hw_stk500.elf urboot.c
```

