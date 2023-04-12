The ATmega1284P exhibits a SWIO baud rate quantisation error of -0.03% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.03% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|472|512|u7.7|`w-udjPr--`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual.hex)|
|472|512|u7.7|`w-udjPr--`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual_pr.hex)|
|508|512|u7.7|`w-udjPr-c`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual_pr_ce.hex)|
|534|768|u7.7|`weudjPr--`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual_pr_ee.hex)|
|578|768|u7.7|`weudjPr-c`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual_pr_ee_ce.hex)|
|560|1024|u7.7|`weudhpr-c`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual_ee_ce_hw.hex)|
|666|1024|u7.7|`wesdhpr-c`|[urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/moteinomega/atmega1284p/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_1s_j1m0_2k4_swio_rxd2_txd3_led%2Bd7_csc7_dual_ee_ce_hw_stk500.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `j1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 1.25%
  + `2k4` shows the fixed communication baud rate, here 2400 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+d7` toggles an active-high (`+`) LED on pin `D7`
  + `csc7` uses pin C7 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr_ce
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr_ee
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr_ee_ce
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw
make MCU=atmega1284p WDTO=1S F_CPU=8100000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfb7 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=76 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfb7 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fd00UL -DRJMPWP=0xcf56 -Wl,--section-start=.text=0x1fd00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=252 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fd00UL -DRJMPWP=0xcf6c -Wl,--section-start=.text=0x1fd00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=208 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xceec -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=482 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcf20 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=378 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_j8m0_19k2_swio_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw_stk500.elf urboot.c
```

