The ATtiny167 exhibits a LINUART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led+b1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny167/watchdog_1_s/external_oscillator_x/%2B2m764800_hz/%2B%2B19k2_baud/uart0_rxa0_txa1/led%2Bb1/urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led%2Bb1.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led+b1_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny167/watchdog_1_s/external_oscillator_x/%2B2m764800_hz/%2B%2B19k2_baud/uart0_rxa0_txa1/led%2Bb1/urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led%2Bb1_pr.hex)|
|286|384|u7.7|`w-u-jPr-c`|[urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led+b1_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny167/watchdog_1_s/external_oscillator_x/%2B2m764800_hz/%2B%2B19k2_baud/uart0_rxa0_txa1/led%2Bb1/urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led%2Bb1_pr_ce.hex)|
|322|384|u7.7|`weu-jPr--`|[urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led+b1_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny167/watchdog_1_s/external_oscillator_x/%2B2m764800_hz/%2B%2B19k2_baud/uart0_rxa0_txa1/led%2Bb1/urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led%2Bb1_pr_ee.hex)|
|348|384|u7.7|`weu-jPr-c`|[urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led+b1_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny167/watchdog_1_s/external_oscillator_x/%2B2m764800_hz/%2B%2B19k2_baud/uart0_rxa0_txa1/led%2Bb1/urboot_t167_1s_x2m7648_19k2_uart0_rxa0_txa1_led%2Bb1_pr_ee_ce.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x2m7648` is F<sub>CPU</sub> of an external oscillator, here 2.7648 MHz
  + `19k2` shows the fixed communication baud rate, here 19200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b1` toggles an active-high (`+`) LED on pin `B1`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny167 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1
make MCU=attiny167 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr
make MCU=attiny167 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr_ce
make MCU=attiny167 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr_ee
make MCU=attiny167 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny167 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -Wl,--relax -nostartfiles -nostdlib -o urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny167 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfa2 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=116 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny167 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb4 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=80 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny167 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc1 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny167 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t167_1s_x11m0592_76k8_uart0_rxa0_txa1_led+b1_pr_ee_ce.elf urboot.c
```

