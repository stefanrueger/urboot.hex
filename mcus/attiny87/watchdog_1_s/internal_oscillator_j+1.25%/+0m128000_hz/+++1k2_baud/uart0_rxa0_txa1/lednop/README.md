The ATtiny87 exhibits a LINUART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr.hex)|
|286|384|u7.7|`w-u-jPr-c`|[urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ce.hex)|
|322|384|u7.7|`weu-jPr--`|[urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee_ce.hex)|

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
  + `j0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 1%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny87 WDTO=1S F_CPU=129600L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop
make MCU=attiny87 WDTO=1S F_CPU=129600L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr
make MCU=attiny87 WDTO=1S F_CPU=129600L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ce
make MCU=attiny87 WDTO=1S F_CPU=129600L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee
make MCU=attiny87 WDTO=1S F_CPU=129600L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfa2 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=116 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb4 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=80 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc1 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_1s_j0m128_1k2_uart0_rxa0_txa1_lednop_pr_ee_ce.elf urboot.c
```

