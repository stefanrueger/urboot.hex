The AT90CAN128 exhibits a SWIO baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|344|512|u8.0|`w-U-jPr--`|[urboot_at90can128.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/internal_oscillator/1062500_hz/4800_baud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128.hex)|
|344|512|u8.0|`w-U-jPr--`|[urboot_at90can128_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/internal_oscillator/1062500_hz/4800_baud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr.hex)|
|396|512|u8.0|`w-U-jPr-c`|[urboot_at90can128_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/internal_oscillator/1062500_hz/4800_baud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr_ce.hex)|
|400|512|u8.0|`weU-jPr--`|[urboot_at90can128_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/internal_oscillator/1062500_hz/4800_baud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr_ee.hex)|
|452|512|u8.0|`weU-jPr-c`|[urboot_at90can128_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/internal_oscillator/1062500_hz/4800_baud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr_ee_ce.hex)|
|434|1024|u8.0|`weU-hpr-c`|[urboot_at90can128_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/internal_oscillator/1062500_hz/4800_baud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_ee_ce_hw.hex)|

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
make MCU=at90can128 WDTO=1S F_CPU=8500000L BAUD_RATE=38400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5
make MCU=at90can128 WDTO=1S F_CPU=8500000L BAUD_RATE=38400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr
make MCU=at90can128 WDTO=1S F_CPU=8500000L BAUD_RATE=38400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr_ce
make MCU=at90can128 WDTO=1S F_CPU=8500000L BAUD_RATE=38400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr_ee
make MCU=at90can128 WDTO=1S F_CPU=8500000L BAUD_RATE=38400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr_ee_ce
make MCU=at90can128 WDTO=1S F_CPU=8500000L BAUD_RATE=38400 SWIO=1 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=186 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=168 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf87 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=116 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf89 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=112 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa3 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=60 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcea3 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=590 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_n8m0_38k4_swio_rxe0_txe1_led+b5_ee_ce_hw.elf urboot.c
```

