The ATmega324P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jPr--`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0.hex)|
|252|256|u7.7|`w-u-jPr--`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0_pr.hex)|
|290|384|u7.7|`w-u-jPr-c`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0_pr_ce.hex)|
|326|384|u7.7|`weu-jPr--`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0_pr_ee.hex)|
|352|384|u7.7|`weu-jPr-c`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0_pr_ee_ce.hex)|
|334|512|u7.7|`weu-hpr-c`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0_ee_ce_hw.hex)|
|438|512|u7.7|`wes-hpr-c`|[urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led+b0_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324p/watchdog_1_s/external_oscillator/%2B5m000000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324p_1s_x5m0_125k0_uart0_rxd0_txd1_led%2Bb0_ee_ce_hw_stk500.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x5m0` is F<sub>CPU</sub> of an external oscillator, here 5.0 MHz
  + `125k0` shows the fixed communication baud rate, here 125000 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b0` toggles an active-high (`+`) LED on pin `B0`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr_ce
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr_ee
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr_ee_ce
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_ee_ce_hw
make MCU=atmega324p WDTO=1S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa2 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=112 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb4 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=76 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=50 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf81 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=196 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfb4 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324p_1s_x20m0_500k0_uart0_rxd0_txd1_led+b0_ee_ce_hw_stk500.elf urboot.c
```

