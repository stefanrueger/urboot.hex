The ATmega64HVE2 exhibits a LINUART baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jPr--`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led.hex)|
|254|256|u7.7|`w-u-jPr--`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr.hex)|
|292|384|u7.7|`w-u-jPr-c`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr_ce.hex)|
|328|384|u7.7|`weu-jPr--`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr_ee.hex)|
|354|384|u7.7|`weu-jPr-c`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_pr_ee_ce.hex)|
|336|1024|u7.7|`weu-hpr-c`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_ee_ce_hw.hex)|
|440|1024|u7.7|`wes-hpr-c`|[urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/external_oscillator/%2B3m000000_hz/%2B%2B57k6_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_x3m0_57k6_uart0_rxb1_txb3_no-led_ee_ce_hw_stk500.hex)|

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
  + `x3m0` is F<sub>CPU</sub> of an external oscillator, here 3.0 MHz
  + `57k6` shows the fixed communication baud rate, here 57600 baud
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
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr_ce
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr_ee
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr_ee_ce
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_ee_ce_hw
make MCU=atmega64hve2 WDTO=2S F_CPU=24000000L BAUD_RATE=460800 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=4 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=4 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfa3 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=110 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfb5 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=74 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfc2 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=48 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce82 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=706 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xceb5 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=604 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=460800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_x24m0_460k8_uart0_rxb1_txb3_no-led_ee_ce_hw_stk500.elf urboot.c
```

