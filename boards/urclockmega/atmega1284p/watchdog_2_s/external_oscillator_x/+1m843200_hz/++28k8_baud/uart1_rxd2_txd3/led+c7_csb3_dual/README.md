The ATmega1284P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|436|512|u7.7|`w-udjPr--`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual.hex)|
|436|512|u7.7|`w-udjPr--`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual_pr.hex)|
|480|512|u7.7|`w-udjPr-c`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual_pr_ce.hex)|
|498|512|u7.7|`weudjPr--`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual_pr_ee.hex)|
|542|768|u7.7|`weudjPr-c`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual_pr_ee_ce.hex)|
|524|1024|u7.7|`weudhpr-c`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual_ee_ce_hw.hex)|
|630|1024|u7.7|`wesdhpr-c`|[urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led+c7_csb3_dual_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B28k8_baud/uart1_rxd2_txd3/led%2Bc7_csb3_dual/urboot_m1284p_2s_x1m8432_28k8_uart1_rxd2_txd3_led%2Bc7_csb3_dual_ee_ce_hw_stk500.hex)|

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
  + `x1m8432` is F<sub>CPU</sub> of an external oscillator, here 1.8432 MHz
  + `28k8` shows the fixed communication baud rate, here 28800 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+c7` toggles an active-high (`+`) LED on pin `C7`
  + `csb3` uses pin B3 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ce
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ee
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ee_ce
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_ee_ce_hw
make MCU=atmega1284p WDTO=2S F_CPU=16000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa5 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=112 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa5 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=50 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fd00UL -DRJMPWP=0xcf5a -Wl,--section-start=.text=0x1fd00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=244 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xceda -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=518 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcf0e -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=414 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x16m0_250k0_uart1_rxd2_txd3_led+c7_csb3_dual_ee_ce_hw_stk500.elf urboot.c
```

