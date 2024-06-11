The ATmega88PB exhibits a SWIO baud rate quantisation error of -0.11% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.11% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-hpr--`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_hw.hex)|
|256|256|u7.7|`w-u-jpr--`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led.hex)|
|290|320|u7.7|`w-u-jPr--`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr.hex)|
|316|320|u7.7|`w-u-jPr-c`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ce.hex)|
|352|384|u7.7|`weu-jPr--`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee.hex)|
|378|384|u7.7|`weu-jPr-c`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee_ce.hex)|
|360|512|u7.7|`weu-hpr-c`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw.hex)|
|464|512|u7.7|`wes-hpr-c`|[urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega88pb/watchdog_1_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/no-led/urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.hex)|

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
  + `m8m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 8.0 MHz + 5.00%
  + `19k2` shows the fixed communication baud rate, here 19200 baud
  + `swio` software I/O (not UART)
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
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_hw
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ce
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee_ce
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw
make MCU=atmega88pb WDTO=1S F_CPU=8400000L BAUD_RATE=19200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=2 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=2 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf97 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=152 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=48 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=8400000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_1s_m8m0_19k2_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.elf urboot.c
```

