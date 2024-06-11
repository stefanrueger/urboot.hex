The ATmega48 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|248|256|u8.0|`w---jPr--`|[urboot_atmega48.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48/watchdog_2_s/external_oscillator/14745600_hz/460800_baud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega48.hex)|
|248|256|u8.0|`w---jPr--`|[urboot_atmega48_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48/watchdog_2_s/external_oscillator/14745600_hz/460800_baud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega48_pr.hex)|
|256|256|u8.0|`w---jPr-c`|[urboot_atmega48_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48/watchdog_2_s/external_oscillator/14745600_hz/460800_baud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega48_pr_ce.hex)|
|304|320|u8.0|`we--jPr--`|[urboot_atmega48_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48/watchdog_2_s/external_oscillator/14745600_hz/460800_baud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega48_pr_ee.hex)|
|320|320|u8.0|`we--jPr-c`|[urboot_atmega48_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48/watchdog_2_s/external_oscillator/14745600_hz/460800_baud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega48_pr_ee_ce.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr_ce
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr_ee
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_576k0_uart0_rxd0_txd1_led+b5_pr_ee_ce.elf urboot.c
```

