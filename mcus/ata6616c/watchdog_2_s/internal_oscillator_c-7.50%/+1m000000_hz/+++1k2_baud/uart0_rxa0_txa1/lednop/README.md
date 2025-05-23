The ATA6616C exhibits a LINUART baud rate quantisation error of +0.11% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.11% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6616c/watchdog_2_s/internal_oscillator_c-7.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6616c/watchdog_2_s/internal_oscillator_c-7.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr.hex)|
|256|256|u8.0|`w---jPr-c`|[urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6616c/watchdog_2_s/internal_oscillator_c-7.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6616c/watchdog_2_s/internal_oscillator_c-7.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr_ee.hex)|
|382|384|u8.0|`weU-jPr-c`|[urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6616c/watchdog_2_s/internal_oscillator_c-7.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxa0_txa1/lednop/urboot_a6616c_2s_c1m0_1k2_uart0_rxa0_txa1_lednop_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `c1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 7.50%
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
make MCU=ata6616c WDTO=2S F_CPU=7400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop
make MCU=ata6616c WDTO=2S F_CPU=7400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr
make MCU=ata6616c WDTO=2S F_CPU=7400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr_ce
make MCU=ata6616c WDTO=2S F_CPU=7400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr_ee
make MCU=ata6616c WDTO=2S F_CPU=7400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6616c -DF_CPU=7400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6616c -DF_CPU=7400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6616c -DF_CPU=7400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb8 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6616c -DF_CPU=7400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6616c -DF_CPU=7400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6616c_2s_c8m0_9k6_uart0_rxa0_txa1_lednop_pr_ee_ce.elf urboot.c
```

