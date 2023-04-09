The AT90USB1287 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr.hex)|
|312|512|u7.7|`w-u-jPr-c`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr_ce.hex)|
|330|512|u7.7|`weu-jPr--`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr_ee.hex)|
|374|512|u7.7|`weu-jPr-c`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_pr_ee_ce.hex)|
|356|1024|u7.7|`weu-hpr-c`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_ee_ce_hw.hex)|
|462|1024|u7.7|`wes-hpr-c`|[urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb1287/watchdog_2_s/external_oscillator/+4m608000_hz/+115k2_baud/uart0_rxd2_txd3/no-led/urboot_usb1287_2s_x4m608_115k2_uart0_rxd2_txd3_no-led_ee_ce_hw_stk500.hex)|

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
  + `x4m608` is F<sub>CPU</sub> of an external oscillator, here 4.608 MHz
  + `115k2` shows the fixed communication baud rate, here 115200 baud
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
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr_ce
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr_ee
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr_ee_ce
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_ee_ce_hw
make MCU=at90usb1287 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6a -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=218 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf73 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=200 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf89 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=156 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce89 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=686 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcebd -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=582 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb1287 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb1287_2s_x20m0_500k0_uart0_rxd2_txd3_no-led_ee_ce_hw_stk500.elf urboot.c
```

