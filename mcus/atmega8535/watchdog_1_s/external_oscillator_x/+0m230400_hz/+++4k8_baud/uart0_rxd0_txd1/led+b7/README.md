The ATmega8535 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|240|256|u8.0|`w---jPr--`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7.hex)|
|240|256|u8.0|`w---jPr--`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7_pr.hex)|
|252|256|u8.0|`w-U-hpr--`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7_hw.hex)|
|256|256|u8.0|`w---jPr-c`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7_pr_ce.hex)|
|300|320|u8.0|`we--jPr--`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7_pr_ee.hex)|
|318|320|u8.0|`we--jPr-c`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7_pr_ee_ce.hex)|
|374|512|u8.0|`weU-hpr-c`|[urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8535/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m8535_1s_x0m2304_4k8_uart0_rxd0_txd1_led%2Bb7_ee_ce_hw.hex)|

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
  + `x0m2304` is F<sub>CPU</sub> of an external oscillator, here 0.2304 MHz
  + `4k8` shows the fixed communication baud rate, here 4800 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b7` toggles an active-high (`+`) LED on pin `B7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_hw
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr_ce
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr_ee
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr_ee_ce
make MCU=atmega8535 WDTO=1S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf87 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=138 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8535 -DF_CPU=24000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8535_1s_x24m0_500k0_uart0_rxd0_txd1_led+b7_ee_ce_hw.elf urboot.c
```

