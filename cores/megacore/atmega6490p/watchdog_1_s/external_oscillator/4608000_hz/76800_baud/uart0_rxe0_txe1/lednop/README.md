The ATmega6490P exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jpr--`|[urboot_atmega6490p.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega6490p/watchdog_1_s/external_oscillator/4608000_hz/76800_baud/uart0_rxe0_txe1/lednop/urboot_atmega6490p.hex)|
|328|512|u8.0|`w-U-jPr--`|[urboot_atmega6490p_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega6490p/watchdog_1_s/external_oscillator/4608000_hz/76800_baud/uart0_rxe0_txe1/lednop/urboot_atmega6490p_pr.hex)|
|370|512|u8.0|`w-U-jPr-c`|[urboot_atmega6490p_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega6490p/watchdog_1_s/external_oscillator/4608000_hz/76800_baud/uart0_rxe0_txe1/lednop/urboot_atmega6490p_pr_ce.hex)|
|384|512|u8.0|`weU-jPr--`|[urboot_atmega6490p_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega6490p/watchdog_1_s/external_oscillator/4608000_hz/76800_baud/uart0_rxe0_txe1/lednop/urboot_atmega6490p_pr_ee.hex)|
|426|512|u8.0|`weU-jPr-c`|[urboot_atmega6490p_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega6490p/watchdog_1_s/external_oscillator/4608000_hz/76800_baud/uart0_rxe0_txe1/lednop/urboot_atmega6490p_pr_ee_ce.hex)|
|412|1024|u8.0|`weU-hpr-c`|[urboot_atmega6490p_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega6490p/watchdog_1_s/external_oscillator/4608000_hz/76800_baud/uart0_rxe0_txe1/lednop/urboot_atmega6490p_ee_ce_hw.hex)|

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
make MCU=atmega6490p WDTO=1S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop
make MCU=atmega6490p WDTO=1S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr
make MCU=atmega6490p WDTO=1S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr_ce
make MCU=atmega6490p WDTO=1S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr_ee
make MCU=atmega6490p WDTO=1S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr_ee_ce
make MCU=atmega6490p WDTO=1S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega6490p -DF_CPU=4608000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf6c -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=184 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega6490p -DF_CPU=4608000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf81 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=142 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega6490p -DF_CPU=4608000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf88 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=128 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega6490p -DF_CPU=4608000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf9d -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=86 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega6490p -DF_CPU=4608000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce9d -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=612 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega6490p -DF_CPU=4608000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m6490p_1s_x4m608_76k8_swio_rxe0_txe1_lednop_ee_ce_hw.elf urboot.c
```

