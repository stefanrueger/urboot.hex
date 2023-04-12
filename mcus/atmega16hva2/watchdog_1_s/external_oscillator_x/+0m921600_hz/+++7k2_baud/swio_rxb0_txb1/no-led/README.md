The ATmega16HVA2 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led.hex)|
|288|384|u7.7|`w-u-jPr--`|[urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr.hex)|
|314|384|u7.7|`w-u-jPr-c`|[urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|346|384|u7.7|`weu-jPr--`|[urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr_ee.hex)|
|372|384|u7.7|`weu-jPr-c`|[urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator_x/%2B0m921600_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x0m9216_7k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x0m9216` is F<sub>CPU</sub> of an external oscillator, here 0.9216 MHz
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega16hva2 WDTO=1S F_CPU=16000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led
make MCU=atmega16hva2 WDTO=1S F_CPU=16000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr
make MCU=atmega16hva2 WDTO=1S F_CPU=16000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr_ce
make MCU=atmega16hva2 WDTO=1S F_CPU=16000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr_ee
make MCU=atmega16hva2 WDTO=1S F_CPU=16000000L BAUD_RATE=125000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfa3 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=114 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb0 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=88 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc0 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=56 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x16m0_125k0_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
```

