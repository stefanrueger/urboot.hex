The ATtiny84 exhibits a SWIO baud rate quantisation error of +0.13% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.13% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led+a4.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B9k6_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led%2Ba4.hex)|
|280|320|u7.7|`w-u-jPr--`|[urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led+a4_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B9k6_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led%2Ba4_pr.hex)|
|306|320|u7.7|`w-u-jPr-c`|[urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led+a4_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B9k6_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led%2Ba4_pr_ce.hex)|
|348|384|u7.7|`weu-jPr--`|[urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led+a4_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B9k6_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led%2Ba4_pr_ee.hex)|
|374|384|u7.7|`weu-jPr-c`|[urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led+a4_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny84/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B9k6_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_2s_x7m3728_9k6_swio_rxa3_txa2_led%2Ba4_pr_ee_ce.hex)|

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
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x7m3728` is F<sub>CPU</sub> of an external oscillator, here 7.3728 MHz
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+a4` toggles an active-high (`+`) LED on pin `A4`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny84 WDTO=2S F_CPU=22118400L BAUD_RATE=28800 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4
make MCU=attiny84 WDTO=2S F_CPU=22118400L BAUD_RATE=28800 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr
make MCU=attiny84 WDTO=2S F_CPU=22118400L BAUD_RATE=28800 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr_ce
make MCU=attiny84 WDTO=2S F_CPU=22118400L BAUD_RATE=28800 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr_ee
make MCU=attiny84 WDTO=2S F_CPU=22118400L BAUD_RATE=28800 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=40 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=28800 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_2s_x22m1184_28k8_swio_rxa3_txa2_led+a4_pr_ee_ce.elf urboot.c
```

