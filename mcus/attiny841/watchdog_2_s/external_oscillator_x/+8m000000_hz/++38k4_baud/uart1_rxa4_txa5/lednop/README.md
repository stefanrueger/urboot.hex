The ATtiny841 exhibits a UART baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B8m000000_hz/%2B%2B38k4_baud/uart1_rxa4_txa5/lednop/urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B8m000000_hz/%2B%2B38k4_baud/uart1_rxa4_txa5/lednop/urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr.hex)|
|286|320|u7.7|`w-u-jPr-c`|[urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B8m000000_hz/%2B%2B38k4_baud/uart1_rxa4_txa5/lednop/urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr_ce.hex)|
|314|320|u7.7|`weu-jPr--`|[urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B8m000000_hz/%2B%2B38k4_baud/uart1_rxa4_txa5/lednop/urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr_ee.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B8m000000_hz/%2B%2B38k4_baud/uart1_rxa4_txa5/lednop/urboot_t841_2s_x8m0_38k4_uart1_rxa4_txa5_lednop_pr_ee_ce.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x8m0` is F<sub>CPU</sub> of an external oscillator, here 8.0 MHz
  + `38k4` shows the fixed communication baud rate, here 38400 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny841 WDTO=2S F_CPU=24000000L BAUD_RATE=115200 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop
make MCU=attiny841 WDTO=2S F_CPU=24000000L BAUD_RATE=115200 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr
make MCU=attiny841 WDTO=2S F_CPU=24000000L BAUD_RATE=115200 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr_ce
make MCU=attiny841 WDTO=2S F_CPU=24000000L BAUD_RATE=115200 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr_ee
make MCU=attiny841 WDTO=2S F_CPU=24000000L BAUD_RATE=115200 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=115200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=115200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=115200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=115200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=115200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x24m0_115k2_uart1_rxa4_txa5_lednop_pr_ee_ce.elf urboot.c
```

