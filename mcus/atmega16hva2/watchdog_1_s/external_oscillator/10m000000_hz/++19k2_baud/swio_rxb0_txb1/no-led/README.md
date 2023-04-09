The ATmega16HVA2 exhibits a SWIO baud rate quantisation error of -0.03% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.03% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator/10m000000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led.hex)|
|282|384|u7.7|`w-u-jPr--`|[urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator/10m000000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr.hex)|
|308|384|u7.7|`w-u-jPr-c`|[urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator/10m000000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|340|384|u7.7|`weu-jPr--`|[urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator/10m000000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr_ee.hex)|
|366|384|u7.7|`weu-jPr-c`|[urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega16hva2/watchdog_1_s/external_oscillator/10m000000_hz/%2B%2B19k2_baud/swio_rxb0_txb1/no-led/urboot_m16hva2_1s_x10m0_19k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|

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
  + `x10m0` is F<sub>CPU</sub> of an external oscillator, here 10.0 MHz
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
make MCU=atmega16hva2 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led
make MCU=atmega16hva2 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr
make MCU=atmega16hva2 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr_ce
make MCU=atmega16hva2 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr_ee
make MCU=atmega16hva2 WDTO=1S F_CPU=20000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=4 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfa0 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=120 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfbd -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=62 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega16hva2 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m16hva2_1s_x20m0_38k4_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
```

