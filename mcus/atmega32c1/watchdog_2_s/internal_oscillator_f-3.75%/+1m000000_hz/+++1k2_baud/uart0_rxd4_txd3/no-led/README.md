The ATmega32C1 exhibits a LINUART baud rate quantisation error of -0.11% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.11% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr.hex)|
|284|384|u7.7|`w-u-jPr-c`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr_ce.hex)|
|320|384|u7.7|`weu-jPr--`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr_ee.hex)|
|346|384|u7.7|`weu-jPr-c`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_pr_ee_ce.hex)|
|328|512|u7.7|`weu-hpr-c`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_ee_ce_hw.hex)|
|432|512|u7.7|`wes-hpr-c`|[urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega32c1/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd4_txd3/no-led/urboot_m32c1_2s_f1m0_1k2_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.hex)|

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
  + `f1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 3.75%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
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
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr_ce
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr_ee
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr_ee_ce
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_ee_ce_hw
make MCU=atmega32c1 WDTO=2S F_CPU=7700000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa8 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=100 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfba -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=64 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf87 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=184 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=80 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega32c1 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_m32c1_2s_f8m0_9k6_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.elf urboot.c
```

