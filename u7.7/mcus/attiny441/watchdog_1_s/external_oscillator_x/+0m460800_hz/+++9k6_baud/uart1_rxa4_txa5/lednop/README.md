The ATtiny441 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_1_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B9k6_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_1_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B9k6_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr.hex)|
|286|320|u7.7|`w-u-jPr-c`|[urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_1_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B9k6_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr_ce.hex)|
|314|320|u7.7|`weu-jPr--`|[urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_1_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B9k6_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr_ee.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_1_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B9k6_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_x0m4608_9k6_uart1_rxa4_txa5_lednop_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x0m4608` is F<sub>CPU</sub> of an external oscillator, here 0.4608 MHz
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny441 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop
make MCU=attiny441 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr
make MCU=attiny441 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr_ce
make MCU=attiny441 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr_ee
make MCU=attiny441 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_x24m0_500k0_uart1_rxa4_txa5_lednop_pr_ee_ce.elf urboot.c
```

