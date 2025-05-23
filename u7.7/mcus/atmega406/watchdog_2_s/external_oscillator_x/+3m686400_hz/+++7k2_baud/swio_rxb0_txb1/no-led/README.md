The ATmega406 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|280|384|u7.7|`w-u-jPr--`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led.hex)|
|280|384|u7.7|`w-u-jPr--`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr.hex)|
|306|384|u7.7|`w-u-jPr-c`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|342|384|u7.7|`weu-jPr--`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr_ee.hex)|
|368|384|u7.7|`weu-jPr-c`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|
|364|512|u7.7|`weu-hpr-c`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_ee_ce_hw.hex)|
|466|512|u7.7|`wes-hpr-c`|[urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega406/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m406_2s_x3m6864_7k2_swio_rxb0_txb1_no-led_ee_ce_hw_stk500.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x3m6864` is F<sub>CPU</sub> of an external oscillator, here 3.6864 MHz
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr_ce
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr_ee
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr_ee_ce
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_ee_ce_hw
make MCU=atmega406 WDTO=2S F_CPU=14745600L BAUD_RATE=28800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x9e80UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x9e80 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x9e80UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x9e80 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x9e80UL -DRJMPWP=0xcfba -Wl,--section-start=.text=0x9e80 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=78 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x9e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x9e80 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x9e80UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x9e80 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x9e00UL -DRJMPWP=0xcf99 -Wl,--section-start=.text=0x9e00 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=148 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x9e00UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x9e00 -Wl,--section-start=.version=0x9ffa -DFRILLS=6 -D_urboot_AVAILABLE=46 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega406 -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m406_2s_x14m7456_28k8_swio_rxb0_txb1_no-led_ee_ce_hw_stk500.elf urboot.c
```

