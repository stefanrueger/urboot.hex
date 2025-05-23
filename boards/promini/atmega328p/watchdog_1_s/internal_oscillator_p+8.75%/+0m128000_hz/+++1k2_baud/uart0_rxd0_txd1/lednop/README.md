The ATmega328P exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jpr--`|[urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/lednop/urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop.hex)|
|332|384|u8.0|`w-U-jPr--`|[urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/lednop/urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr.hex)|
|368|384|u8.0|`we--jPr-c`|[urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/lednop/urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee_ce.hex)|
|378|384|u8.0|`w-U-jPr-c`|[urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/lednop/urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ce.hex)|
|378|384|u8.0|`weU-jPr--`|[urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/lednop/urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee.hex)|
|416|512|u8.0|`weU-hpr-c`|[urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/promini/atmega328p/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/lednop/urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_ee_ce_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `p0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 8.75%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop
make MCU=atmega328p WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr
make MCU=atmega328p WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee_ce
make MCU=atmega328p WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ce
make MCU=atmega328p WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee
make MCU=atmega328p WDTO=1S F_CPU=139200L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa9 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=52 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc0 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=9 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf9c -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=96 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=139200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_1s_p0m128_1k2_swio_rxd0_txd1_lednop_ee_ce_hw.elf urboot.c
```

