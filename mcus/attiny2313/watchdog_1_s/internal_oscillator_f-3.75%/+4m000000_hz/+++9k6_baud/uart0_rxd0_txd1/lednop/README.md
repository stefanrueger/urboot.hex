The ATtiny2313 exhibits a UART baud rate quantisation error of +0.26% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.26% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|222|224|u8.0|`w---jPr--`|[urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/internal_oscillator_f-3.75%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop.hex)|
|222|224|u8.0|`w---jPr--`|[urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/internal_oscillator_f-3.75%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr.hex)|
|250|256|u8.0|`w---jPr-c`|[urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/internal_oscillator_f-3.75%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr_ce.hex)|
|288|288|u8.0|`we--jPr--`|[urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/internal_oscillator_f-3.75%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr_ee.hex)|
|310|320|u8.0|`we--jPr-c`|[urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/internal_oscillator_f-3.75%25/%2B4m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_1s_f4m0_9k6_uart0_rxd0_txd1_lednop_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `f4m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 4.0 MHz - 3.75%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny2313 WDTO=1S F_CPU=7700000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop
make MCU=attiny2313 WDTO=1S F_CPU=7700000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr
make MCU=attiny2313 WDTO=1S F_CPU=7700000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr_ce
make MCU=attiny2313 WDTO=1S F_CPU=7700000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee
make MCU=attiny2313 WDTO=1S F_CPU=7700000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=4 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=7700000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=7700000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x700UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x700 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=7700000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x6e0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x6e0 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=7700000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x6c0UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x6c0 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=7700000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_f8m0_19k2_uart0_rxd0_txd1_lednop_pr_ee_ce.elf urboot.c
```

