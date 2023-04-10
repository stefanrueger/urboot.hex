The AT90SCR100 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPr--`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr.hex)|
|280|512|u7.7|`w-u-jPr-c`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr_ce.hex)|
|318|512|u7.7|`weu-jPr--`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr_ee.hex)|
|328|512|u7.7|`weu-hpr-c`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_ee_ce_hw.hex)|
|342|512|u7.7|`weu-jPr-c`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_pr_ee_ce.hex)|
|432|512|u7.7|`wes-hpr-c`|[urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/external_oscillator_x/%2B1m382400_hz/%2B%2B%2B7k2_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_x1m3824_7k2_uart0_rxd0_txd1_no-led_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x1m3824` is F<sub>CPU</sub> of an external oscillator, here 1.3824 MHz
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ce
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_ee_ce_hw
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee_ce
make MCU=at90scr100 WDTO=2S F_CPU=24000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf60 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=250 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf73 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=212 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf7f -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=202 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf7f -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=188 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcfb2 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=100 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=125000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_x24m0_125k0_uart0_rxd0_txd1_no-led_ee_ce_hw_stk500.elf urboot.c
```

