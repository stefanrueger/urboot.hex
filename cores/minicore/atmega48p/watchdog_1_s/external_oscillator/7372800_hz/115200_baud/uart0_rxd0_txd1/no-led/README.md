The ATmega48P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---jPr--`|[urboot_atmega48p.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/watchdog_1_s/external_oscillator/7372800_hz/115200_baud/uart0_rxd0_txd1/no-led/urboot_atmega48p.hex)|
|246|256|u8.0|`w---jPr--`|[urboot_atmega48p_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/watchdog_1_s/external_oscillator/7372800_hz/115200_baud/uart0_rxd0_txd1/no-led/urboot_atmega48p_pr.hex)|
|256|256|u8.0|`w---jPr-c`|[urboot_atmega48p_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/watchdog_1_s/external_oscillator/7372800_hz/115200_baud/uart0_rxd0_txd1/no-led/urboot_atmega48p_pr_ce.hex)|
|302|320|u8.0|`we--jPr--`|[urboot_atmega48p_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/watchdog_1_s/external_oscillator/7372800_hz/115200_baud/uart0_rxd0_txd1/no-led/urboot_atmega48p_pr_ee.hex)|
|320|320|u8.0|`we--jPr-c`|[urboot_atmega48p_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega48p/watchdog_1_s/external_oscillator/7372800_hz/115200_baud/uart0_rxd0_txd1/no-led/urboot_atmega48p_pr_ee_ce.hex)|

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
make MCU=atmega48p WDTO=1S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led
make MCU=atmega48p WDTO=1S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr
make MCU=atmega48p WDTO=1S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr_ce
make MCU=atmega48p WDTO=1S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr_ee
make MCU=atmega48p WDTO=1S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_1s_x16m0_250k0_uart0_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
```

