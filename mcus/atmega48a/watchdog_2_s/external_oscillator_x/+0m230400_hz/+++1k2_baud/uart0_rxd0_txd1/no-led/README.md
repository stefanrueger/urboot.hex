The ATmega48A exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u7.7|`w-u-jPr--`|[urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48a/watchdog_2_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/no-led/urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led.hex)|
|246|256|u7.7|`w-u-jPr--`|[urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48a/watchdog_2_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/no-led/urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr.hex)|
|256|256|u7.7|`w-u-jPr-c`|[urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48a/watchdog_2_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/no-led/urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr_ce.hex)|
|312|320|u7.7|`weu-jPr--`|[urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48a/watchdog_2_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/no-led/urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr_ee.hex)|
|320|320|u7.7|`weu-jPr-c`|[urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48a/watchdog_2_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/no-led/urboot_m48a_2s_x0m2304_1k2_uart0_rxd0_txd1_no-led_pr_ee_ce.hex)|

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
  + `x0m2304` is F<sub>CPU</sub> of an external oscillator, here 0.2304 MHz
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega48a WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led
make MCU=atmega48a WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr
make MCU=atmega48a WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ce
make MCU=atmega48a WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee
make MCU=atmega48a WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48a -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48a -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=2 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48a -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfcf -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48a -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48a -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48a_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
```

