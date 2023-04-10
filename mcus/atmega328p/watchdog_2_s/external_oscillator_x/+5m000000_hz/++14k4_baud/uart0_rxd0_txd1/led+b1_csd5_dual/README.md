The ATmega328P exhibits a UART baud rate quantisation error of -1.36% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 1.36% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|382|384|u7.7|`w-udjpr--`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual.hex)|
|406|512|u7.7|`w-udjPr--`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr.hex)|
|432|512|u7.7|`w-udjPr-c`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr_ce.hex)|
|472|512|u7.7|`weudjPr--`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr_ee.hex)|
|484|512|u7.7|`weudhpr-c`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual_ee_ce_hw.hex)|
|498|512|u7.7|`weudjPr-c`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr_ee_ce.hex)|
|588|1024|u7.7|`wesdhpr-c`|[urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B5m000000_hz/%2B%2B14k4_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x5m0_14k4_uart0_rxd0_txd1_led%2Bb1_csd5_dual_ee_ce_hw_stk500.hex)|

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
  + `x5m0` is F<sub>CPU</sub> of an external oscillator, here 5.0 MHz
  + `14k4` shows the fixed communication baud rate, here 14400 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b1` toggles an active-high (`+`) LED on pin `B1`
  + `csd5` uses pin D5 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce
make MCU=atmega328p WDTO=2S F_CPU=20000000L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf9b -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=124 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfa8 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=98 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfbc -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=46 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7c00UL -DRJMPWP=0xcefc -Wl,--section-start=.text=0x7c00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=456 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x20m0_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw_stk500.elf urboot.c
```

