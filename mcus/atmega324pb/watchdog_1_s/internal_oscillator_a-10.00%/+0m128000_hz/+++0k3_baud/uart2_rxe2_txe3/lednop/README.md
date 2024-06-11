The ATmega324PB exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_1_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart2_rxe2_txe3/lednop/urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_1_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart2_rxe2_txe3/lednop/urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_1_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart2_rxe2_txe3/lednop/urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_1_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart2_rxe2_txe3/lednop/urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_1_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart2_rxe2_txe3/lednop/urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_1_s/internal_oscillator_a-10.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart2_rxe2_txe3/lednop/urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_ee_ce_hw.hex)|

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
  + `a0m128` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.128 MHz - 10.00%
  + `0k3` shows the fixed communication baud rate, here 300 baud
  + `uart2` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega324pb WDTO=1S F_CPU=115200L BAUD_RATE=300 UARTNUM=2 RX=AtmelPE2 TX=AtmelPE3 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop
make MCU=atmega324pb WDTO=1S F_CPU=115200L BAUD_RATE=300 UARTNUM=2 RX=AtmelPE2 TX=AtmelPE3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr
make MCU=atmega324pb WDTO=1S F_CPU=115200L BAUD_RATE=300 UARTNUM=2 RX=AtmelPE2 TX=AtmelPE3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ce
make MCU=atmega324pb WDTO=1S F_CPU=115200L BAUD_RATE=300 UARTNUM=2 RX=AtmelPE2 TX=AtmelPE3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee
make MCU=atmega324pb WDTO=1S F_CPU=115200L BAUD_RATE=300 UARTNUM=2 RX=AtmelPE2 TX=AtmelPE3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee_ce
make MCU=atmega324pb WDTO=1S F_CPU=115200L BAUD_RATE=300 UARTNUM=2 RX=AtmelPE2 TX=AtmelPE3 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=115200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=2 -DTX=AtmelPE3 -DRX=AtmelPE2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=115200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=2 -DTX=AtmelPE3 -DRX=AtmelPE2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=115200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=2 -DTX=AtmelPE3 -DRX=AtmelPE2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=115200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=2 -DTX=AtmelPE3 -DRX=AtmelPE2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=115200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=2 -DTX=AtmelPE3 -DRX=AtmelPE2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=115200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=2 -DTX=AtmelPE3 -DRX=AtmelPE2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_1s_a0m128_0k3_uart2_rxe2_txe3_lednop_ee_ce_hw.elf urboot.c
```

