The ATmega64HVE2 exhibits a LINUART baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|248|256|u8.0|`w---jPr--`|[urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led.hex)|
|248|256|u8.0|`w---jPr--`|[urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr.hex)|
|354|384|u8.0|`w-U-jPr-c`|[urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ce.hex)|
|364|384|u8.0|`weU-jPr--`|[urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee.hex)|
|370|384|u8.0|`weU-jPr-c`|[urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee_ce.hex)|
|392|1024|u8.0|`weU-hpr-c`|[urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega64hve2/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxb1_txb3/no-led/urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_ee_ce_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `n8m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 8.0 MHz + 6.25%
  + `38k4` shows the fixed communication baud rate, here 38400 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega64hve2 WDTO=2S F_CPU=8500000L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led
make MCU=atmega64hve2 WDTO=2S F_CPU=8500000L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr
make MCU=atmega64hve2 WDTO=2S F_CPU=8500000L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ce
make MCU=atmega64hve2 WDTO=2S F_CPU=8500000L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee
make MCU=atmega64hve2 WDTO=2S F_CPU=8500000L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee_ce
make MCU=atmega64hve2 WDTO=2S F_CPU=8500000L BAUD_RATE=38400 UARTNUM=0 RX=AtmelPB1 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=4 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=4 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfb4 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfb9 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe80UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0xfe80 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce90 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=632 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega64hve2 -DF_CPU=8500000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPB3 -DRX=AtmelPB1 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m64hve2_2s_n8m0_38k4_uart0_rxb1_txb3_no-led_ee_ce_hw.elf urboot.c
```

