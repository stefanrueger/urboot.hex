The ATtiny841 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u7.7|`w-u-jPr--`|[urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B1m000000_hz/%2B125k0_baud/uart0_alt1_rxb2_txa7/no-led/urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led.hex)|
|252|256|u7.7|`w-u-jPr--`|[urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B1m000000_hz/%2B125k0_baud/uart0_alt1_rxb2_txa7/no-led/urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr.hex)|
|290|320|u7.7|`w-u-jPr-c`|[urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B1m000000_hz/%2B125k0_baud/uart0_alt1_rxb2_txa7/no-led/urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr_ce.hex)|
|318|320|u7.7|`weu-jPr--`|[urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B1m000000_hz/%2B125k0_baud/uart0_alt1_rxb2_txa7/no-led/urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr_ee.hex)|
|352|384|u7.7|`weu-jPr-c`|[urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B1m000000_hz/%2B125k0_baud/uart0_alt1_rxb2_txa7/no-led/urboot_t841_1s_x1m0_125k0_uart0_alt1_rxb2_txa7_no-led_pr_ee_ce.hex)|

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
  + `x1m0` is F<sub>CPU</sub> of an external oscillator, here 1.0 MHz
  + `125k0` shows the fixed communication baud rate, here 125000 baud
  + `uart0` UART number
  + `alt1` alternative RX/TX pin assignment
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny841 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led
make MCU=attiny841 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr
make MCU=attiny841 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr_ce
make MCU=attiny841 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr_ee
make MCU=attiny841 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x8m0_1000k0_uart0_alt1_rxb2_txa7_no-led_pr_ee_ce.elf urboot.c
```

