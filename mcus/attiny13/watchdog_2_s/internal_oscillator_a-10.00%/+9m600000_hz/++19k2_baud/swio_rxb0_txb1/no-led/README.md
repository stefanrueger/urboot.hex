The ATtiny13 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_a-10.00%25/%2B9m600000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_a-10.00%25/%2B9m600000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr.hex)|
|286|288|u7.7|`w-u-jPr-c`|[urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_a-10.00%25/%2B9m600000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|322|352|u7.7|`weu-jPr--`|[urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_a-10.00%25/%2B9m600000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee.hex)|
|350|352|u7.7|`weu-jPr-c`|[urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_2_s/internal_oscillator_a-10.00%25/%2B9m600000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `a9m6` is F<sub>CPU</sub> of a too slow internal oscillator, here 9.6 MHz - 10.00%
  + `19k2` shows the fixed communication baud rate, here 19200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13 WDTO=2S F_CPU=8640000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led
make MCU=attiny13 WDTO=2S F_CPU=8640000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr
make MCU=attiny13 WDTO=2S F_CPU=8640000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ce
make MCU=attiny13 WDTO=2S F_CPU=8640000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee
make MCU=attiny13 WDTO=2S F_CPU=8640000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=2 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=8640000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=2 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=8640000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=8640000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=8640000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=8640000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_2s_a9m6_19k2_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
```

