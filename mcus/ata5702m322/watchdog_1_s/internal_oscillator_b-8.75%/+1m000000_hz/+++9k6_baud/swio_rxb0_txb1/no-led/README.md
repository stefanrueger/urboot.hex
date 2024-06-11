The ATA5702M322 exhibits a SWIO baud rate quantisation error of +0.05% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.05% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jPr--`|[urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/internal_oscillator_b-8.75%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/internal_oscillator_b-8.75%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr.hex)|
|304|320|u8.0|`w---jPr-c`|[urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/internal_oscillator_b-8.75%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ce.hex)|
|320|320|u8.0|`we--jPr--`|[urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/internal_oscillator_b-8.75%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee.hex)|
|360|384|u8.0|`we--jPr-c`|[urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5702m322/watchdog_1_s/internal_oscillator_b-8.75%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `a5702m322` is F<sub>CPU</sub> of a too slow internal oscillator, here 5702.322 MHz - 10.00%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5702m322 WDTO=1S F_CPU=912500L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led
make MCU=ata5702m322 WDTO=1S F_CPU=912500L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr
make MCU=ata5702m322 WDTO=1S F_CPU=912500L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ce
make MCU=ata5702m322 WDTO=1S F_CPU=912500L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee
make MCU=ata5702m322 WDTO=1S F_CPU=912500L BAUD_RATE=9600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=0 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=912500L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=912500L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7ec0UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x7ec0 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=912500L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7ec0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x7ec0 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=912500L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5702m322 -DF_CPU=912500L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5702m322_1s_b1m0_9k6_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
```

