The AT90CAN128 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jpr--`|[urboot_at90can128.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128.hex)|
|278|512|u7.7|`w-u-jPr--`|[urboot_at90can128_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128_pr.hex)|
|322|512|u7.7|`w-u-jPr-c`|[urboot_at90can128_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128_pr_ce.hex)|
|338|512|u7.7|`weu-jPr--`|[urboot_at90can128_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128_pr_ee.hex)|
|382|512|u7.7|`weu-jPr-c`|[urboot_at90can128_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128_pr_ee_ce.hex)|
|364|1024|u7.7|`weu-hpr-c`|[urboot_at90can128_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128_ee_ce_hw.hex)|
|470|1024|u7.7|`wes-hpr-c`|[urboot_at90can128_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/cores/megacore/at90can128/watchdog_2_s/external_oscillator/5529600_hz/57600_baud/uart0_rxe0_txe1/lednop/urboot_at90can128_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
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
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr_ce
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr_ee
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr_ee_ce
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_ee_ce_hw
make MCU=at90can128 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf62 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=234 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf78 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=190 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf80 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=174 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf96 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=130 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce96 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=660 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcecb -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=554 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_2s_x24m0_250k0_uart0_rxe0_txe1_lednop_ee_ce_hw_stk500.elf urboot.c
```

