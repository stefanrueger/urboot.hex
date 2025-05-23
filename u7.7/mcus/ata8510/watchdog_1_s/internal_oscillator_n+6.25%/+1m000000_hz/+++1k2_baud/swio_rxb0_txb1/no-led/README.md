The ATA8510 exhibits a SWIO baud rate quantisation error of -0.19% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.19% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr.hex)|
|254|256|u7.7|`w-u-jpr--`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led.hex)|
|298|320|u7.7|`w-u-jPr-c`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|320|320|u7.7|`weu-jPr--`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee.hex)|
|360|384|u7.7|`weu-jPr-c`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|
|330|20464|u7.7|`-eu-hpr-c`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_ee_ce_hw.hex)|
|434|20464|u7.7|`-es-hpr-c`|[urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/ata8510/watchdog_1_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a8510_1s_n1m0_1k2_swio_rxb0_txb1_no-led_ee_ce_hw_stk500.hex)|

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
  + `n1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 6.25%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
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
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr_ce
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr_ee
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr_ee_ce
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 PGMWRITEPAGE=0 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_ee_ce_hw
make MCU=ata8510 WDTO=1S F_CPU=8500000L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 PGMWRITEPAGE=0 NAME=urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x4f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x4f00 -Wl,--section-start=.version=0x4ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x4f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x4f00 -Wl,--section-start=.version=0x4ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x4ec0UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x4ec0 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x4ec0UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x4ec0 -Wl,--section-start=.version=0x4ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x4e80UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x4e80 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x0UL -DRJMPWP=0x9508 -Wl,--section-start=.text=0x0 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=20134 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x0UL -DRJMPWP=0x9508 -Wl,--section-start=.text=0x0 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=20030 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata8510 -DF_CPU=8500000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a8510_1s_n8m0_9k6_swio_rxb0_txb1_no-led_ee_ce_hw_stk500.elf urboot.c
```

