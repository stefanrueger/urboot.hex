The ATmega48 exhibits a UART baud rate quantisation error of -0.27% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.27% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_atmega48.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega48/watchdog_1_s/internal_oscillator/900000_hz/2400_baud/uart0_rxd0_txd1/lednop/urboot_atmega48.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_atmega48_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega48/watchdog_1_s/internal_oscillator/900000_hz/2400_baud/uart0_rxd0_txd1/lednop/urboot_atmega48_pr.hex)|
|286|320|u7.7|`w-u-jPr-c`|[urboot_atmega48_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega48/watchdog_1_s/internal_oscillator/900000_hz/2400_baud/uart0_rxd0_txd1/lednop/urboot_atmega48_pr_ce.hex)|
|314|320|u7.7|`weu-jPr--`|[urboot_atmega48_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega48/watchdog_1_s/internal_oscillator/900000_hz/2400_baud/uart0_rxd0_txd1/lednop/urboot_atmega48_pr_ee.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot_atmega48_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/minicore/atmega48/watchdog_1_s/internal_oscillator/900000_hz/2400_baud/uart0_rxd0_txd1/lednop/urboot_atmega48_pr_ee_ce.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega48 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop
make MCU=atmega48 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr
make MCU=atmega48 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr_ce
make MCU=atmega48 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee
make MCU=atmega48 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_1s_a8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee_ce.elf urboot.c
```

