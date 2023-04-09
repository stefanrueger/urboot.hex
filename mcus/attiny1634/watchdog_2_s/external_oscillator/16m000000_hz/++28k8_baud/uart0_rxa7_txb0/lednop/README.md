The ATtiny1634 exhibits a UART baud rate quantisation error of -0.80% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.80% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u7.7|`w-u-jPr--`|[urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/external_oscillator/16m000000_hz/%2B%2B28k8_baud/uart0_rxa7_txb0/lednop/urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop.hex)|
|246|256|u7.7|`w-u-jPr--`|[urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/external_oscillator/16m000000_hz/%2B%2B28k8_baud/uart0_rxa7_txb0/lednop/urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr.hex)|
|256|256|u7.7|`w-u-jPr-c`|[urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/external_oscillator/16m000000_hz/%2B%2B28k8_baud/uart0_rxa7_txb0/lednop/urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ce.hex)|
|312|384|u7.7|`weu-jPr--`|[urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/external_oscillator/16m000000_hz/%2B%2B28k8_baud/uart0_rxa7_txb0/lednop/urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee.hex)|
|338|384|u7.7|`weu-jPr-c`|[urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/external_oscillator/16m000000_hz/%2B%2B28k8_baud/uart0_rxa7_txb0/lednop/urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee_ce.hex)|

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
  + `x16m0` is F<sub>CPU</sub> of an external oscillator, here 16.0 MHz
  + `28k8` shows the fixed communication baud rate, here 28800 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny1634 WDTO=2S F_CPU=16000000L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPA7 TX=AtmelPB0 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop
make MCU=attiny1634 WDTO=2S F_CPU=16000000L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPA7 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr
make MCU=attiny1634 WDTO=2S F_CPU=16000000L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPA7 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ce
make MCU=attiny1634 WDTO=2S F_CPU=16000000L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPA7 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee
make MCU=attiny1634 WDTO=2S F_CPU=16000000L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPA7 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB0 -DRX=AtmelPA7 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB0 -DRX=AtmelPA7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=2 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB0 -DRX=AtmelPA7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfac -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=90 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB0 -DRX=AtmelPA7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb9 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=64 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB0 -DRX=AtmelPA7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x16m0_28k8_uart0_rxa7_txb0_lednop_pr_ee_ce.elf urboot.c
```

