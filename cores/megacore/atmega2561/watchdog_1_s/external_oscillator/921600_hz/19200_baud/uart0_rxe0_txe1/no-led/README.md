The ATmega2561 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jPr--`|[urboot_atmega2561.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega2561/watchdog_1_s/external_oscillator/921600_hz/19200_baud/uart0_rxe0_txe1/no-led/urboot_atmega2561.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_atmega2561_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega2561/watchdog_1_s/external_oscillator/921600_hz/19200_baud/uart0_rxe0_txe1/no-led/urboot_atmega2561_pr.hex)|
|356|512|u8.0|`w-U-jPr-c`|[urboot_atmega2561_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega2561/watchdog_1_s/external_oscillator/921600_hz/19200_baud/uart0_rxe0_txe1/no-led/urboot_atmega2561_pr_ce.hex)|
|360|512|u8.0|`weU-jPr--`|[urboot_atmega2561_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega2561/watchdog_1_s/external_oscillator/921600_hz/19200_baud/uart0_rxe0_txe1/no-led/urboot_atmega2561_pr_ee.hex)|
|412|512|u8.0|`weU-jPr-c`|[urboot_atmega2561_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega2561/watchdog_1_s/external_oscillator/921600_hz/19200_baud/uart0_rxe0_txe1/no-led/urboot_atmega2561_pr_ee_ce.hex)|
|394|1024|u8.0|`weU-hpr-c`|[urboot_atmega2561_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/atmega2561/watchdog_1_s/external_oscillator/921600_hz/19200_baud/uart0_rxe0_txe1/no-led/urboot_atmega2561_ee_ce_hw.hex)|

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
make MCU=atmega2561 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led
make MCU=atmega2561 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr
make MCU=atmega2561 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr_ce
make MCU=atmega2561 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr_ee
make MCU=atmega2561 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr_ee_ce
make MCU=atmega2561 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3ff00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x3ff00 -Wl,--section-start=.version=0x3fffa -DFRILLS=4 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3ff00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x3ff00 -Wl,--section-start=.version=0x3fffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf73 -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=10 -D_urboot_AVAILABLE=156 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf75 -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=10 -D_urboot_AVAILABLE=152 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf8f -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=10 -D_urboot_AVAILABLE=100 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3fc00UL -DRJMPWP=0xce8f -Wl,--section-start=.text=0x3fc00 -Wl,--section-start=.version=0x3fffa -DFRILLS=10 -D_urboot_AVAILABLE=630 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_1s_x24m0_500k0_uart0_rxe0_txe1_no-led_ee_ce_hw.elf urboot.c
```

