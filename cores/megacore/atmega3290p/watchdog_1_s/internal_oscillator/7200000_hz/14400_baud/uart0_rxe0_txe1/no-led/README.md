The ATmega3290P exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jpr--`|[urboot_atmega3290p.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega3290p/watchdog_1_s/internal_oscillator/7200000_hz/14400_baud/uart0_rxe0_txe1/no-led/urboot_atmega3290p.hex)|
|334|384|u8.0|`w-U-jPr--`|[urboot_atmega3290p_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega3290p/watchdog_1_s/internal_oscillator/7200000_hz/14400_baud/uart0_rxe0_txe1/no-led/urboot_atmega3290p_pr.hex)|
|370|384|u8.0|`we--jPr-c`|[urboot_atmega3290p_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega3290p/watchdog_1_s/internal_oscillator/7200000_hz/14400_baud/uart0_rxe0_txe1/no-led/urboot_atmega3290p_pr_ee_ce.hex)|
|380|384|u8.0|`w-U-jPr-c`|[urboot_atmega3290p_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega3290p/watchdog_1_s/internal_oscillator/7200000_hz/14400_baud/uart0_rxe0_txe1/no-led/urboot_atmega3290p_pr_ce.hex)|
|380|384|u8.0|`weU-jPr--`|[urboot_atmega3290p_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega3290p/watchdog_1_s/internal_oscillator/7200000_hz/14400_baud/uart0_rxe0_txe1/no-led/urboot_atmega3290p_pr_ee.hex)|
|418|512|u8.0|`weU-hpr-c`|[urboot_atmega3290p_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega3290p/watchdog_1_s/internal_oscillator/7200000_hz/14400_baud/uart0_rxe0_txe1/no-led/urboot_atmega3290p_ee_ce_hw.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega3290p WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led
make MCU=atmega3290p WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr
make MCU=atmega3290p WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr_ee_ce
make MCU=atmega3290p WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr_ce
make MCU=atmega3290p WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr_ee
make MCU=atmega3290p WDTO=1S F_CPU=7200000L BAUD_RATE=14400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe1 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290p -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfaa -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=50 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290p -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd3 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290p -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290p -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=9 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290p -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf9d -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega3290p -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m3290p_1s_a8m0_14k4_swio_rxe0_txe1_no-led_ee_ce_hw.elf urboot.c
```

