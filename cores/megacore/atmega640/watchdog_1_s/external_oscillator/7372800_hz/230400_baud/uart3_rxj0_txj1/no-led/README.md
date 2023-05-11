The ATmega640 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|248|256|u7.7|`w-u-jPr--`|[urboot_atmega640.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640.hex)|
|248|256|u7.7|`w-u-jPr--`|[urboot_atmega640_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640_pr.hex)|
|256|256|u7.7|`w-u-jPr-c`|[urboot_atmega640_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640_pr_ce.hex)|
|310|512|u7.7|`weu-jPr--`|[urboot_atmega640_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640_pr_ee.hex)|
|334|512|u7.7|`weu-jPr-c`|[urboot_atmega640_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640_pr_ee_ce.hex)|
|320|1024|u7.7|`weu-hpr-c`|[urboot_atmega640_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640_ee_ce_hw.hex)|
|424|1024|u7.7|`wes-hpr-c`|[urboot_atmega640_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega640/watchdog_1_s/external_oscillator/7372800_hz/230400_baud/uart3_rxj0_txj1/no-led/urboot_atmega640_ee_ce_hw_stk500.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr_ce
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr_ee
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr_ee_ce
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_ee_ce_hw
make MCU=atmega640 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=3 RX=AtmelPJ0 TX=AtmelPJ1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=2 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf78 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=202 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf84 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=178 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce84 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=704 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xceb8 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=600 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=3 -DTX=AtmelPJ1 -DRX=AtmelPJ0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_x18m432_576k0_uart3_rxj0_txj1_no-led_ee_ce_hw_stk500.elf urboot.c
```

