The ATtiny13 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jPr--`|[urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B1m200000_hz/%2B%2B%2B1k8_baud/swio_rxb1_txb0/no-led/urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led.hex)|
|254|256|u8.0|`w---jPr--`|[urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B1m200000_hz/%2B%2B%2B1k8_baud/swio_rxb1_txb0/no-led/urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr.hex)|
|280|288|u8.0|`w---jPr-c`|[urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B1m200000_hz/%2B%2B%2B1k8_baud/swio_rxb1_txb0/no-led/urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr_ce.hex)|
|316|320|u8.0|`we--jPr--`|[urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B1m200000_hz/%2B%2B%2B1k8_baud/swio_rxb1_txb0/no-led/urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr_ee.hex)|
|346|352|u8.0|`we--jPr-c`|[urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13/watchdog_1_s/internal_oscillator_p%2B8.75%25/%2B1m200000_hz/%2B%2B%2B1k8_baud/swio_rxb1_txb0/no-led/urboot_t13_1s_p1m2_1k8_swio_rxb1_txb0_no-led_pr_ee_ce.hex)|

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
  + `p1m2` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.2 MHz + 8.75%
  + `1k8` shows the fixed communication baud rate, here 1800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13 WDTO=1S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led
make MCU=attiny13 WDTO=1S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr
make MCU=attiny13 WDTO=1S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr_ce
make MCU=attiny13 WDTO=1S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr_ee
make MCU=attiny13 WDTO=1S F_CPU=10440000L BAUD_RATE=14400 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2c0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x2c0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=5 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13 -DF_CPU=10440000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13_1s_p9m6_14k4_swio_rxb1_txb0_no-led_pr_ee_ce.elf urboot.c
```

