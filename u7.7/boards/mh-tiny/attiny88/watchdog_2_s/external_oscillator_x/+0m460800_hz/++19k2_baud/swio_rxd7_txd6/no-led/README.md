The ATtiny88 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B19k2_baud/swio_rxd7_txd6/no-led/urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B19k2_baud/swio_rxd7_txd6/no-led/urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr.hex)|
|298|320|u7.7|`w-u-jPr-c`|[urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B19k2_baud/swio_rxd7_txd6/no-led/urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr_ce.hex)|
|316|320|u7.7|`weu-jPr--`|[urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B19k2_baud/swio_rxd7_txd6/no-led/urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr_ee.hex)|
|356|384|u7.7|`weu-jPr-c`|[urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/mh-tiny/attiny88/watchdog_2_s/external_oscillator_x/%2B0m460800_hz/%2B%2B19k2_baud/swio_rxd7_txd6/no-led/urboot_t88_2s_x0m4608_19k2_swio_rxd7_txd6_no-led_pr_ee_ce.hex)|

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
  + `x0m4608` is F<sub>CPU</sub> of an external oscillator, here 0.4608 MHz
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
make MCU=attiny88 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led
make MCU=attiny88 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr
make MCU=attiny88 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr_ce
make MCU=attiny88 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr_ee
make MCU=attiny88 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 SWIO=1 RX=AtmelPD7 TX=AtmelPD6 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny88 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD6 -DRX=AtmelPD7 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t88_2s_x24m0_1000k0_swio_rxd7_txd6_no-led_pr_ee_ce.elf urboot.c
```

