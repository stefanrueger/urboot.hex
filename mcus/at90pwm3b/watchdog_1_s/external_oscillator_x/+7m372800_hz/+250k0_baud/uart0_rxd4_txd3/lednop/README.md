The AT90PWM3B exhibits a SWIO baud rate quantisation error of +1.69% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 1.69% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|294|320|u7.7|`w-u-jPr--`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop.hex)|
|294|320|u7.7|`w-u-jPr--`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr.hex)|
|320|320|u7.7|`w-u-jPr-c`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr_ce.hex)|
|356|384|u7.7|`weu-jPr--`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr_ee.hex)|
|382|384|u7.7|`weu-jPr-c`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_pr_ee_ce.hex)|
|276|512|u7.7|`w-u-hpr--`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_hw.hex)|
|364|512|u7.7|`weu-hpr-c`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_ee_ce_hw.hex)|
|468|512|u7.7|`wes-hpr-c`|[urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm3b/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxd4_txd3/lednop/urboot_pwm3b_1s_x7m3728_250k0_swio_rxd4_txd3_lednop_ee_ce_hw_stk500.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x7m3728` is F<sub>CPU</sub> of an external oscillator, here 7.3728 MHz
  + `250k0` shows the fixed communication baud rate, here 250000 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr_ce
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr_ee
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr_ee_ce
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_hw
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_ee_ce_hw
make MCU=at90pwm3b WDTO=1S F_CPU=14745600L BAUD_RATE=500000 SWIO=1 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=44 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc3 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=46 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf64 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=254 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf90 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=166 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcfc3 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=64 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=14745600L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=500000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_1s_x14m7456_500k0_swio_rxd4_txd3_lednop_ee_ce_hw_stk500.elf urboot.c
```

