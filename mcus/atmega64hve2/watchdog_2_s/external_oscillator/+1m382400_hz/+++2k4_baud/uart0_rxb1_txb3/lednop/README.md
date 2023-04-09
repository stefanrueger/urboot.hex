The ATmega64HVE2 exhibits a LINUART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr.hex)|
|298|384|u7.7|`w-u-jPr-c`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr_ce.hex)|
|334|384|u7.7|`weu-jPr--`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr_ee.hex)|
|360|384|u7.7|`weu-jPr-c`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_pr_ee_ce.hex)|
|342|1024|u7.7|`weu-hpr-c`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_ee_ce_hw.hex)|
|446|1024|u7.7|`wes-hpr-c`|[urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B1m382400_hz/%2B%2B%2B2k4_baud/uart0_rxb1_txb3/lednop/urboot_m64hve2_2s_x1m3824_2k4_uart0_rxb1_txb3_lednop_ee_ce_hw_stk500.hex)|

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
  + `x1m3824` is F<sub>CPU</sub> of an external oscillator, here 1.3824 MHz
  + `2k4` shows the fixed communication baud rate, here 2400 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr_ce
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr_ee
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr_ee_ce
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_ee_ce_hw
make MCU=atmega64hve2 WDTO=2S F_CPU=22118400L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=3 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfa6 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfb8 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=68 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce85 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=700 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xceb8 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=598 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x22m1184_38k4_uart0_rxb1_txb3_lednop_ee_ce_hw_stk500.elf urboot.c
```

