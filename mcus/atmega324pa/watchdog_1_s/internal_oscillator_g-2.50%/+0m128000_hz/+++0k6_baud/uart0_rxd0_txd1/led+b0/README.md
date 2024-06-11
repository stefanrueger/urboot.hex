The ATmega324PA exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pa/watchdog_1_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led%2Bb0.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pa/watchdog_1_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led%2Bb0_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pa/watchdog_1_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led%2Bb0_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pa/watchdog_1_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led%2Bb0_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pa/watchdog_1_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led%2Bb0_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pa/watchdog_1_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led%2Bb0_ee_ce_hw.hex)|

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
  + `g0m128` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.128 MHz - 2.50%
  + `0k6` shows the fixed communication baud rate, here 600 baud
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
make MCU=atmega324pa WDTO=1S F_CPU=124800L BAUD_RATE=600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0
make MCU=atmega324pa WDTO=1S F_CPU=124800L BAUD_RATE=600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr
make MCU=atmega324pa WDTO=1S F_CPU=124800L BAUD_RATE=600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ce
make MCU=atmega324pa WDTO=1S F_CPU=124800L BAUD_RATE=600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ee
make MCU=atmega324pa WDTO=1S F_CPU=124800L BAUD_RATE=600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ee_ce
make MCU=atmega324pa WDTO=1S F_CPU=124800L BAUD_RATE=600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pa -DF_CPU=124800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pa -DF_CPU=124800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pa -DF_CPU=124800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pa -DF_CPU=124800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pa -DF_CPU=124800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pa -DF_CPU=124800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pa_1s_g0m128_0k6_uart0_rxd0_txd1_led+b0_ee_ce_hw.elf urboot.c
```

