The ATmega640 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jPr--`|[urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega640/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/led%2Bb7/urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led%2Bb7.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega640/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/led%2Bb7/urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led%2Bb7_pr.hex)|
|360|512|u8.0|`w-U-jPr-c`|[urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega640/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/led%2Bb7/urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led%2Bb7_pr_ce.hex)|
|374|512|u8.0|`weU-jPr--`|[urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega640/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/led%2Bb7/urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led%2Bb7_pr_ee.hex)|
|416|512|u8.0|`weU-jPr-c`|[urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega640/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/led%2Bb7/urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led%2Bb7_pr_ee_ce.hex)|
|402|1024|u8.0|`weU-hpr-c`|[urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega640/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/led%2Bb7/urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led%2Bb7_ee_ce_hw.hex)|

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
  + `l0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 3.75%
  + `0k6` shows the fixed communication baud rate, here 600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b7` toggles an active-high (`+`) LED on pin `B7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega640 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7
make MCU=atmega640 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr
make MCU=atmega640 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ce
make MCU=atmega640 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ee
make MCU=atmega640 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ee_ce
make MCU=atmega640 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=0 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf7c -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=152 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf83 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=138 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf98 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=96 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce98 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=622 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega640 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m640_1s_l0m128_0k6_swio_rxe0_txe1_led+b7_ee_ce_hw.elf urboot.c
```

