The ATmega64M1 exhibits a LINUART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jPr--`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led.hex)|
|252|256|u7.7|`w-u-jPr--`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr.hex)|
|276|512|u7.7|`w-u-jPr-c`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr_ce.hex)|
|314|512|u7.7|`weu-jPr--`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr_ee.hex)|
|338|512|u7.7|`weu-jPr-c`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_pr_ee_ce.hex)|
|324|1024|u7.7|`weu-hpr-c`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_ee_ce_hw.hex)|
|428|1024|u7.7|`wes-hpr-c`|[urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega64m1/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B%2B14k4_baud/uart0_rxd4_txd3/no-led/urboot_m64m1_1s_x7m3728_14k4_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.hex)|

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
  + `x7m3728` is F<sub>CPU</sub> of an external oscillator, here 7.3728 MHz
  + `m64m1` is F<sub>CPU</sub> of a too fast internal oscillator, here 64.1 MHz + 5.00%
  + `14k4` shows the fixed communication baud rate, here 14400 baud
  + `uart0` UART number
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
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr_ce
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr_ee
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr_ee_ce
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_ee_ce_hw
make MCU=atmega64m1 WDTO=1S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf67 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=236 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf7a -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=198 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf86 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=174 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce86 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=700 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xceba -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=596 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64m1 -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64m1_1s_x14m7456_28k8_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.elf urboot.c
```

