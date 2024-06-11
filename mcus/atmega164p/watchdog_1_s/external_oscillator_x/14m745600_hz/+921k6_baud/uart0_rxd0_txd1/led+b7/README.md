The ATmega164P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|238|256|u8.0|`w---hpr--`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7_hw.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7_pr.hex)|
|348|384|u8.0|`w-U-jPr-c`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7_pr_ce.hex)|
|358|384|u8.0|`weU-jPr--`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7_pr_ee.hex)|
|384|384|u8.0|`weU-jPr-c`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7_pr_ee_ce.hex)|
|386|512|u8.0|`weU-hpr-c`|[urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164p/watchdog_1_s/external_oscillator_x/14m745600_hz/%2B921k6_baud/uart0_rxd0_txd1/led%2Bb7/urboot_m164p_1s_x14m7456_921k6_uart0_rxd0_txd1_led%2Bb7_ee_ce_hw.hex)|

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
  + `x14m7456` is F<sub>CPU</sub> of an external oscillator, here 14.7456 MHz
  + `921k6` shows the fixed communication baud rate, here 921600 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b7` toggles an active-high (`+`) LED on pin `B7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_hw
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr_ce
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr_ee
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr_ee_ce
make MCU=atmega164p WDTO=1S F_CPU=16000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb6 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf8d -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164p -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164p_1s_x16m0_1000k0_uart0_rxd0_txd1_led+b7_ee_ce_hw.elf urboot.c
```

