The ATmega324A exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jpr--`|[urboot_atmega324a.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/mightycore/atmega324a/watchdog_1_s/internal_oscillator/129600_hz/1200_baud/uart1_rxd2_txd3/led%2Bb0/urboot_atmega324a.hex)|
|330|384|u8.0|`w-U-jPr--`|[urboot_atmega324a_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/mightycore/atmega324a/watchdog_1_s/internal_oscillator/129600_hz/1200_baud/uart1_rxd2_txd3/led%2Bb0/urboot_atmega324a_pr.hex)|
|366|384|u8.0|`we--jPr-c`|[urboot_atmega324a_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/mightycore/atmega324a/watchdog_1_s/internal_oscillator/129600_hz/1200_baud/uart1_rxd2_txd3/led%2Bb0/urboot_atmega324a_pr_ee_ce.hex)|
|376|384|u8.0|`w-U-jPr-c`|[urboot_atmega324a_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/mightycore/atmega324a/watchdog_1_s/internal_oscillator/129600_hz/1200_baud/uart1_rxd2_txd3/led%2Bb0/urboot_atmega324a_pr_ce.hex)|
|376|384|u8.0|`weU-jPr--`|[urboot_atmega324a_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/mightycore/atmega324a/watchdog_1_s/internal_oscillator/129600_hz/1200_baud/uart1_rxd2_txd3/led%2Bb0/urboot_atmega324a_pr_ee.hex)|
|414|512|u8.0|`weU-hpr-c`|[urboot_atmega324a_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/mightycore/atmega324a/watchdog_1_s/internal_oscillator/129600_hz/1200_baud/uart1_rxd2_txd3/led%2Bb0/urboot_atmega324a_ee_ce_hw.hex)|

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
make MCU=atmega324a WDTO=1S F_CPU=129600L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0
make MCU=atmega324a WDTO=1S F_CPU=129600L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr
make MCU=atmega324a WDTO=1S F_CPU=129600L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr_ee_ce
make MCU=atmega324a WDTO=1S F_CPU=129600L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr_ce
make MCU=atmega324a WDTO=1S F_CPU=129600L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr_ee
make MCU=atmega324a WDTO=1S F_CPU=129600L BAUD_RATE=1200 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa8 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=9 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf9b -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=98 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324a -DF_CPU=129600L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324a_1s_j0m128_1k2_swio_rxd2_txd3_led+b0_ee_ce_hw.elf urboot.c
```

