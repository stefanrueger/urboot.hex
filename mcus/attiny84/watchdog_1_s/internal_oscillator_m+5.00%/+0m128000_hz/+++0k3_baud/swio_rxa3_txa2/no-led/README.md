The ATtiny84 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jPr--`|[urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxa3_txa2/no-led/urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxa3_txa2/no-led/urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr.hex)|
|296|320|u8.0|`w---jPr-c`|[urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxa3_txa2/no-led/urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ce.hex)|
|320|320|u8.0|`we--jPr--`|[urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxa3_txa2/no-led/urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee.hex)|
|378|384|u8.0|`weU-jPr-c`|[urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxa3_txa2/no-led/urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `m0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 5.00%
  + `0k3` shows the fixed communication baud rate, here 300 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny84 WDTO=1S F_CPU=134400L BAUD_RATE=300 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led
make MCU=attiny84 WDTO=1S F_CPU=134400L BAUD_RATE=300 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr
make MCU=attiny84 WDTO=1S F_CPU=134400L BAUD_RATE=300 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ce
make MCU=attiny84 WDTO=1S F_CPU=134400L BAUD_RATE=300 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee
make MCU=attiny84 WDTO=1S F_CPU=134400L BAUD_RATE=300 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=134400L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=134400L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=134400L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=134400L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=134400L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_m0m128_0k3_swio_rxa3_txa2_no-led_pr_ee_ce.elf urboot.c
```

