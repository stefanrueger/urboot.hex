The ATmega329PA exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jPr--`|[urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega329pa/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/lednop/urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega329pa/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/lednop/urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr.hex)|
|356|384|u8.0|`w-U-jPr-c`|[urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega329pa/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/lednop/urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr_ce.hex)|
|366|384|u8.0|`weU-jPr--`|[urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega329pa/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/lednop/urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr_ee.hex)|
|372|384|u8.0|`weU-jPr-c`|[urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega329pa/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/lednop/urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_pr_ee_ce.hex)|
|394|512|u8.0|`weU-hpr-c`|[urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega329pa/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/lednop/urboot_m329pa_2s_x5m5296_19k2_uart0_rxe0_txe1_lednop_ee_ce_hw.hex)|

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
  + `x5m5296` is F<sub>CPU</sub> of an external oscillator, here 5.5296 MHz
  + `19k2` shows the fixed communication baud rate, here 19200 baud
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
make MCU=atmega329pa WDTO=2S F_CPU=22118400L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop
make MCU=atmega329pa WDTO=2S F_CPU=22118400L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr
make MCU=atmega329pa WDTO=2S F_CPU=22118400L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr_ce
make MCU=atmega329pa WDTO=2S F_CPU=22118400L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr_ee
make MCU=atmega329pa WDTO=2S F_CPU=22118400L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr_ee_ce
make MCU=atmega329pa WDTO=2S F_CPU=22118400L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega329pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega329pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb5 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega329pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfba -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega329pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega329pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf91 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=118 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega329pa -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m329pa_2s_x22m1184_76k8_uart0_rxe0_txe1_lednop_ee_ce_hw.elf urboot.c
```

