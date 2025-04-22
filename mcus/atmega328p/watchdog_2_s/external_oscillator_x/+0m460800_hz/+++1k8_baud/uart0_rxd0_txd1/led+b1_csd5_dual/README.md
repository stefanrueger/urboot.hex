The ATmega328P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|384|384|u8.1|`w--djPr--`|[urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led+b1_csd5_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B1k8_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led%2Bb1_csd5_dual.hex)|
|384|384|u8.1|`w--djPr--`|[urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led+b1_csd5_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B1k8_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr.hex)|
|488|512|u8.1|`w-UdjPr-c`|[urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B1k8_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr_ce.hex)|
|498|512|u8.1|`weUdjPr--`|[urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B1k8_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr_ee.hex)|
|504|512|u8.1|`weUdjPr-c`|[urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B1k8_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led%2Bb1_csd5_dual_pr_ee_ce.hex)|
|510|512|u8.1|`weUdhpr-c`|[urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega328p/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B%2B1k8_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x0m4608_1k8_uart0_rxd0_txd1_led%2Bb1_csd5_dual_ee_ce_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
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
  + `x0m4608` is F<sub>CPU</sub> of an external oscillator, here 0.4608 MHz
  + `1k8` shows the fixed communication baud rate, here 1800 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b1` toggles an active-high (`+`) LED on pin `B1`
  + `csd5` uses pin D5 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=2S F_CPU=14745600L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual
make MCU=atmega328p WDTO=2S F_CPU=14745600L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr
make MCU=atmega328p WDTO=2S F_CPU=14745600L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=14745600L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=14745600L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce
make MCU=atmega328p WDTO=2S F_CPU=14745600L BAUD_RATE=57600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=2 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=2 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfb9 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfbe -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x14m7456_57k6_uart0_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw.elf urboot.c
```

