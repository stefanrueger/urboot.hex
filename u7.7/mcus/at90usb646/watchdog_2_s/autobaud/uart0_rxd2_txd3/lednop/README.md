Note that autobaud bootloaders normally can only detect host baud rates = f/8, f/16, ... f/2048 +/- 1.5%, where f=F<sub>CPU</sub>. Internal oscillators have a high unknown deviation: baud rates under f/260 are recommended for these.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPra-`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop.hex)|
|256|256|u7.7|`w-u-jPra-`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr.hex)|
|298|512|u7.7|`w-u-jPrac`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ce.hex)|
|336|512|u7.7|`weu-jPra-`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee.hex)|
|360|512|u7.7|`weu-jPrac`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee_ce.hex)|
|346|1024|u7.7|`weu-hprac`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw.hex)|
|450|1024|u7.7|`wes-hprac`|[urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90usb646/watchdog_2_s/autobaud/uart0_rxd2_txd3/lednop/urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw_stk500.hex)|

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
  + `a` autobaud detection (f_cpu/8n using discrete divisors, n = 1, 2, ..., 256)
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `autobaud` detects host baud rate f/8, f/16, f/24, ..., f/2048 (f=F<sub>CPU</sub>)
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
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ce
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee_ce
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw
make MCU=at90usb646 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=0 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf72 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=214 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf85 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=176 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf91 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=152 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce91 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=678 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xcec5 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=574 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb646 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb646_2s_autobaud_uart0_rxd2_txd3_lednop_ee_ce_hw_stk500.elf urboot.c
```

