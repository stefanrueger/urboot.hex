The ATtiny84 exhibits a SWIO baud rate quantisation error of -0.03% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.03% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led+a4.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/luminet/attiny84/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led%2Ba4.hex)|
|282|320|u7.7|`w-u-jPr--`|[urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led+a4_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/luminet/attiny84/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led%2Ba4_pr.hex)|
|308|320|u7.7|`w-u-jPr-c`|[urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led+a4_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/luminet/attiny84/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led%2Ba4_pr_ce.hex)|
|350|384|u7.7|`weu-jPr--`|[urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led+a4_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/luminet/attiny84/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led%2Ba4_pr_ee.hex)|
|376|384|u7.7|`weu-jPr-c`|[urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led+a4_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/luminet/attiny84/watchdog_1_s/internal_oscillator_j%2B1.25%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/swio_rxa3_txa2/led%2Ba4/urboot_t84_1s_j1m0_4k8_swio_rxa3_txa2_led%2Ba4_pr_ee_ce.hex)|

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
  + `j1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 1.25%
  + `4k8` shows the fixed communication baud rate, here 4800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+a4` toggles an active-high (`+`) LED on pin `A4`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny84 WDTO=1S F_CPU=8100000L BAUD_RATE=38400 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4
make MCU=attiny84 WDTO=1S F_CPU=8100000L BAUD_RATE=38400 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr
make MCU=attiny84 WDTO=1S F_CPU=8100000L BAUD_RATE=38400 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr_ce
make MCU=attiny84 WDTO=1S F_CPU=8100000L BAUD_RATE=38400 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr_ee
make MCU=attiny84 WDTO=1S F_CPU=8100000L BAUD_RATE=38400 SWIO=1 RX=AtmelPA3 TX=AtmelPA2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPA4 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe5 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny84 -DF_CPU=8100000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=38400 -DLED=AtmelPA4 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA2 -DRX=AtmelPA3 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t84_1s_j8m0_38k4_swio_rxa3_txa2_led+a4_pr_ee_ce.elf urboot.c
```

