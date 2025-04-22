The ATmega324A exhibits a UART baud rate quantisation error of -0.43% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.43% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led+b0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led%2Bb0.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led+b0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led%2Bb0_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led+b0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led%2Bb0_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led+b0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led%2Bb0_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led+b0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led%2Bb0_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led+b0_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324a_2s_g1m0_1k2_uart0_rxd0_txd1_led%2Bb0_ee_ce_hw.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `g1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 2.50%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b0` toggles an active-high (`+`) LED on pin `B0`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega324a WDTO=2S F_CPU=7800000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0
make MCU=atmega324a WDTO=2S F_CPU=7800000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr
make MCU=atmega324a WDTO=2S F_CPU=7800000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr_ce
make MCU=atmega324a WDTO=2S F_CPU=7800000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr_ee
make MCU=atmega324a WDTO=2S F_CPU=7800000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr_ee_ce
make MCU=atmega324a WDTO=2S F_CPU=7800000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_2s_g8m0_9k6_uart0_rxd0_txd1_led+b0_ee_ce_hw.elf urboot.c
```

