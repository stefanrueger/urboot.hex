The ATmega168P exhibits a UART baud rate quantisation error of +0.07% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.07% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|238|256|u8.0|`w---hpr--`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5_hw.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega168p/watchdog_1_s/internal_oscillator_l%2B3.75%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led%2Bb5_ee_ce_hw.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `l8m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 8.0 MHz + 3.75%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_hw
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ce
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ee
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ee_ce
make MCU=atmega168p WDTO=1S F_CPU=8300000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega168p -DF_CPU=8300000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m168p_1s_l8m0_9k6_uart0_rxd0_txd1_led+b5_ee_ce_hw.elf urboot.c
```

