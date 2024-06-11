The ATmega328PB exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B14k4_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led%2Bb5.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B14k4_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led%2Bb5_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B14k4_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led%2Bb5_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B14k4_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led%2Bb5_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B14k4_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led%2Bb5_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/uno/atmega328pb/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B14k4_baud/uart1_rxb4_txb3/led%2Bb5/urboot_m328pb_1s_x0m2304_14k4_uart1_rxb4_txb3_led%2Bb5_ee_ce_hw.hex)|

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
  + `x0m2304` is F<sub>CPU</sub> of an external oscillator, here 0.2304 MHz
  + `14k4` shows the fixed communication baud rate, here 14400 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328pb WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5
make MCU=atmega328pb WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr
make MCU=atmega328pb WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr_ce
make MCU=atmega328pb WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr_ee
make MCU=atmega328pb WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=1 RX=AtmelPB4 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr_ee_ce
make MCU=atmega328pb WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=1 RX=AtmelPB4 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB3 -DRX=AtmelPB4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328pb_1s_x16m0_1000k0_uart1_rxb4_txb3_led+b5_ee_ce_hw.elf urboot.c
```

