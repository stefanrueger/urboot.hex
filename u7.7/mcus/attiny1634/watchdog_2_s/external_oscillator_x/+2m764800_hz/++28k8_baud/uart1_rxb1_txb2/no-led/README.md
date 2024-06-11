The ATtiny1634 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|248|256|u7.7|`w-u-jPr--`|[urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny1634/watchdog_2_s/external_oscillator_x/%2B2m764800_hz/%2B%2B28k8_baud/uart1_rxb1_txb2/no-led/urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led.hex)|
|248|256|u7.7|`w-u-jPr--`|[urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny1634/watchdog_2_s/external_oscillator_x/%2B2m764800_hz/%2B%2B28k8_baud/uart1_rxb1_txb2/no-led/urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr.hex)|
|256|256|u7.7|`w-u-jPr-c`|[urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny1634/watchdog_2_s/external_oscillator_x/%2B2m764800_hz/%2B%2B28k8_baud/uart1_rxb1_txb2/no-led/urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr_ce.hex)|
|314|384|u7.7|`weu-jPr--`|[urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny1634/watchdog_2_s/external_oscillator_x/%2B2m764800_hz/%2B%2B28k8_baud/uart1_rxb1_txb2/no-led/urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr_ee.hex)|
|340|384|u7.7|`weu-jPr-c`|[urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny1634/watchdog_2_s/external_oscillator_x/%2B2m764800_hz/%2B%2B28k8_baud/uart1_rxb1_txb2/no-led/urboot_t1634_2s_x2m7648_28k8_uart1_rxb1_txb2_no-led_pr_ee_ce.hex)|

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
  + `x2m7648` is F<sub>CPU</sub> of an external oscillator, here 2.7648 MHz
  + `28k8` shows the fixed communication baud rate, here 28800 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny1634 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led
make MCU=attiny1634 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr
make MCU=attiny1634 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr_ce
make MCU=attiny1634 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr_ee
make MCU=attiny1634 WDTO=2S F_CPU=24000000L BAUD_RATE=250000 UARTNUM=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=70 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc3 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=44 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_x24m0_250k0_uart1_rxb1_txb2_no-led_pr_ee_ce.elf urboot.c
```

