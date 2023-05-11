The ATmega328P exhibits a SWIO baud rate quantisation error of -0.19% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.19% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|432|512|u7.7|`w-udjPr--`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual.hex)|
|432|512|u7.7|`w-udjPr--`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr.hex)|
|458|512|u7.7|`w-udjPr-c`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr_ce.hex)|
|498|512|u7.7|`weudjPr--`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr_ee.hex)|
|510|512|u7.7|`weudhpr-c`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_ee_ce_hw.hex)|
|510|512|u7.7|`weudjPr-c`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_pr_ee_ce.hex)|
|614|1024|u7.7|`wesdhpr-c`|[urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_n1m0_1k2_swio_rxd0_txd1_template_dual_ee_ce_hw_stk500.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `n1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 6.25%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
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
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_ee_ce_hw
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr_ee_ce
make MCU=atmega328p WDTO=2S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=80 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfbe -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfdf -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7c00UL -DRJMPWP=0xcf13 -Wl,--section-start=.text=0x7c00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=410 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_n8m0_9k6_swio_rxd0_txd1_template_dual_ee_ce_hw_stk500.elf urboot.c
```

