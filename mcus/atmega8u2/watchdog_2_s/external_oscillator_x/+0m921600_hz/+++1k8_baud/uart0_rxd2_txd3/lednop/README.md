The ATmega8U2 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8u2/watchdog_2_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B1k8_baud/uart0_rxd2_txd3/lednop/urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8u2/watchdog_2_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B1k8_baud/uart0_rxd2_txd3/lednop/urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8u2/watchdog_2_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B1k8_baud/uart0_rxd2_txd3/lednop/urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8u2/watchdog_2_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B1k8_baud/uart0_rxd2_txd3/lednop/urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8u2/watchdog_2_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B1k8_baud/uart0_rxd2_txd3/lednop/urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega8u2/watchdog_2_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B1k8_baud/uart0_rxd2_txd3/lednop/urboot_m8u2_2s_x0m9216_1k8_uart0_rxd2_txd3_lednop_ee_ce_hw.hex)|

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
  + `x0m9216` is F<sub>CPU</sub> of an external oscillator, here 0.9216 MHz
  + `1k8` shows the fixed communication baud rate, here 1800 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega8u2 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop
make MCU=atmega8u2 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr
make MCU=atmega8u2 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr_ce
make MCU=atmega8u2 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr_ee
make MCU=atmega8u2 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr_ee_ce
make MCU=atmega8u2 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8u2 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8u2 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8u2 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8u2 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8u2 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8u2 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=28800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8u2_2s_x14m7456_28k8_uart0_rxd2_txd3_lednop_ee_ce_hw.elf urboot.c
```

