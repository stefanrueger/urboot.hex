The ATtiny13A exhibits a SWIO baud rate quantisation error of +0.28% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.28% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jPr--`|[urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_1_s/internal_oscillator_o%2B7.50%25/%2B9m600000_hz/%2B%2B76k8_baud/swio_rxb1_txb0/no-led/urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_1_s/internal_oscillator_o%2B7.50%25/%2B9m600000_hz/%2B%2B76k8_baud/swio_rxb1_txb0/no-led/urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr.hex)|
|284|288|u8.0|`w---jPr-c`|[urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_1_s/internal_oscillator_o%2B7.50%25/%2B9m600000_hz/%2B%2B76k8_baud/swio_rxb1_txb0/no-led/urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ce.hex)|
|320|320|u8.0|`we--jPr--`|[urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_1_s/internal_oscillator_o%2B7.50%25/%2B9m600000_hz/%2B%2B76k8_baud/swio_rxb1_txb0/no-led/urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee.hex)|
|350|352|u8.0|`we--jPr-c`|[urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny13a/watchdog_1_s/internal_oscillator_o%2B7.50%25/%2B9m600000_hz/%2B%2B76k8_baud/swio_rxb1_txb0/no-led/urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee_ce.hex)|

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
  + `o9m6` is F<sub>CPU</sub> of a too fast internal oscillator, here 9.6 MHz + 7.50%
  + `76k8` shows the fixed communication baud rate, here 76800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny13a WDTO=1S F_CPU=10320000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led
make MCU=attiny13a WDTO=1S F_CPU=10320000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr
make MCU=attiny13a WDTO=1S F_CPU=10320000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ce
make MCU=attiny13a WDTO=1S F_CPU=10320000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee
make MCU=attiny13a WDTO=1S F_CPU=10320000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB0 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10320000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x300UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x300 -Wl,--section-start=.version=0x3fa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10320000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2e0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x2e0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10320000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2c0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x2c0 -Wl,--section-start=.version=0x3fa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10320000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x2a0UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x2a0 -Wl,--section-start=.version=0x3fa -DFRILLS=5 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny13a -DF_CPU=10320000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB0 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t13a_1s_o9m6_76k8_swio_rxb1_txb0_no-led_pr_ee_ce.elf urboot.c
```

