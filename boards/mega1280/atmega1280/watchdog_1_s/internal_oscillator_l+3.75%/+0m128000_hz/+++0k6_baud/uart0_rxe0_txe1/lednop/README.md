The ATmega1280 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jpr--`|[urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/lednop/urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop.hex)|
|336|512|u8.0|`w-U-jPr--`|[urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/lednop/urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr.hex)|
|388|512|u8.0|`w-U-jPr-c`|[urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/lednop/urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ce.hex)|
|392|512|u8.0|`weU-jPr--`|[urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/lednop/urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee.hex)|
|444|512|u8.0|`weU-jPr-c`|[urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/lednop/urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee_ce.hex)|
|426|1024|u8.0|`weU-hpr-c`|[urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxe0_txe1/lednop/urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_ee_ce_hw.hex)|

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
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1280 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop
make MCU=atmega1280 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr
make MCU=atmega1280 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ce
make MCU=atmega1280 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee
make MCU=atmega1280 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee_ce
make MCU=atmega1280 WDTO=1S F_CPU=132800L BAUD_RATE=600 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf69 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=176 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf83 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=124 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf85 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=120 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf9f -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=68 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce9f -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=598 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=132800L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_1s_l0m128_0k6_swio_rxe0_txe1_lednop_ee_ce_hw.elf urboot.c
```

