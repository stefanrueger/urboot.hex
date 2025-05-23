The ATmega168PB exhibits a UART baud rate quantisation error of +1.73% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 1.73% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u7.7|`w-u-hpr--`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_hw.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5.hex)|
|256|256|u7.7|`w-u-jPr--`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_pr.hex)|
|294|384|u7.7|`w-u-jPr-c`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_pr_ce.hex)|
|330|384|u7.7|`weu-jPr--`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_pr_ee.hex)|
|356|384|u7.7|`weu-jPr-c`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_pr_ee_ce.hex)|
|338|512|u7.7|`weu-hpr-c`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_ee_ce_hw.hex)|
|442|512|u7.7|`wes-hpr-c`|[urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega168pb/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led%2Bb5_ee_ce_hw_stk500.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x10m0` is F<sub>CPU</sub> of an external oscillator, here 10.0 MHz
  + `76k8` shows the fixed communication baud rate, here 76800 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_hw
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ce
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ee
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ee_ce
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_ee_ce_hw
make MCU=atmega168pb WDTO=1S F_CPU=10000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=4 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=90 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf8c -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=174 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcfc0 -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=70 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168pb -DF_CPU=10000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168pb_1s_x10m0_76k8_uart0_rxd0_txd1_led+b5_ee_ce_hw_stk500.elf urboot.c
```

