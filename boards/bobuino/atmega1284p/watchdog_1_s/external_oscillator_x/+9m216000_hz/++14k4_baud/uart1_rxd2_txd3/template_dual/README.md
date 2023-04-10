The ATmega1284P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|444|512|u7.7|`w-udjPr--`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual.hex)|
|444|512|u7.7|`w-udjPr--`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr.hex)|
|488|512|u7.7|`w-udjPr-c`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr_ce.hex)|
|504|512|u7.7|`weudjPr--`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr_ee.hex)|
|548|768|u7.7|`weudjPr-c`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_pr_ee_ce.hex)|
|530|1024|u7.7|`weudhpr-c`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_ee_ce_hw.hex)|
|636|1024|u7.7|`wesdhpr-c`|[urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/bobuino/atmega1284p/watchdog_1_s/external_oscillator_x/%2B9m216000_hz/%2B%2B14k4_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_x9m216_14k4_uart1_rxd2_txd3_template_dual_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `d` dual boot (over-the-air programming from external SPI flash)
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x9m216` is F<sub>CPU</sub> of an external oscillator, here 9.216 MHz
  + `14k4` shows the fixed communication baud rate, here 14400 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `template` bootloaders contains `mov rx,rx` nops as placeholders for LED and CS operations
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr_ce
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr_ee
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr_ee_ce
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_ee_ce_hw
make MCU=atmega1284p WDTO=1S F_CPU=18432000L BAUD_RATE=28800 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa9 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa9 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=86 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fd00UL -DRJMPWP=0xcf5d -Wl,--section-start=.text=0x1fd00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=238 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcedd -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=512 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcf11 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=408 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x18m432_28k8_uart1_rxd2_txd3_template_dual_ee_ce_hw_stk500.elf urboot.c
```

