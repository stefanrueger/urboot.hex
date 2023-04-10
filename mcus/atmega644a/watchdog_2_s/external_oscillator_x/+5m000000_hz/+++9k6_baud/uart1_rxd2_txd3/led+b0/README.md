The ATmega644A exhibits a UART baud rate quantisation error of -1.36% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 1.36% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0_pr.hex)|
|278|512|u7.7|`w-u-jPr-c`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0_pr_ce.hex)|
|316|512|u7.7|`weu-jPr--`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0_pr_ee.hex)|
|340|512|u7.7|`weu-jPr-c`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0_pr_ee_ce.hex)|
|326|1024|u7.7|`weu-hpr-c`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0_ee_ce_hw.hex)|
|430|1024|u7.7|`wes-hpr-c`|[urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led+b0_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega644a/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb0/urboot_m644a_2s_x5m0_9k6_uart1_rxd2_txd3_led%2Bb0_ee_ce_hw_stk500.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x5m0` is F<sub>CPU</sub> of an external oscillator, here 5.0 MHz
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `uart1` UART number
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
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr_ce
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr_ee
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr_ee_ce
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_ee_ce_hw
make MCU=atmega644a WDTO=2S F_CPU=20000000L BAUD_RATE=38400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd3 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd3 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf5f -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=252 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf72 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=214 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf7e -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=190 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce7e -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=716 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xceb1 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=614 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644a -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644a_2s_x20m0_38k4_uart1_rxd2_txd3_led+b0_ee_ce_hw_stk500.elf urboot.c
```

