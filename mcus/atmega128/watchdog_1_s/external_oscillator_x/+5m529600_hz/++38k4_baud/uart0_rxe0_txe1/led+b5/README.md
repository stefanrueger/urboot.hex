The ATmega128 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|248|256|u8.0|`w---jPr--`|[urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega128/watchdog_1_s/external_oscillator_x/%2B5m529600_hz/%2B%2B38k4_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led%2Bb5.hex)|
|248|256|u8.0|`w---jPr--`|[urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega128/watchdog_1_s/external_oscillator_x/%2B5m529600_hz/%2B%2B38k4_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led%2Bb5_pr.hex)|
|354|512|u8.0|`w-U-jPr-c`|[urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega128/watchdog_1_s/external_oscillator_x/%2B5m529600_hz/%2B%2B38k4_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led%2Bb5_pr_ce.hex)|
|358|512|u8.0|`weU-jPr--`|[urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega128/watchdog_1_s/external_oscillator_x/%2B5m529600_hz/%2B%2B38k4_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led%2Bb5_pr_ee.hex)|
|410|512|u8.0|`weU-jPr-c`|[urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega128/watchdog_1_s/external_oscillator_x/%2B5m529600_hz/%2B%2B38k4_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led%2Bb5_pr_ee_ce.hex)|
|392|1024|u8.0|`weU-hpr-c`|[urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega128/watchdog_1_s/external_oscillator_x/%2B5m529600_hz/%2B%2B38k4_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m128_1s_x5m5296_38k4_uart0_rxe0_txe1_led%2Bb5_ee_ce_hw.hex)|

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
  + `x5m5296` is F<sub>CPU</sub> of an external oscillator, here 5.5296 MHz
  + `38k4` shows the fixed communication baud rate, here 38400 baud
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
make MCU=atmega128 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5
make MCU=atmega128 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr
make MCU=atmega128 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr_ce
make MCU=atmega128 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr_ee
make MCU=atmega128 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr_ee_ce
make MCU=atmega128 WDTO=1S F_CPU=11059200L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=26 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega128 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega128 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf70 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=158 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega128 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf72 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=154 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega128 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf8c -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=102 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega128 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce8c -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=632 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega128 -DF_CPU=11059200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m128_1s_x11m0592_76k8_uart0_rxe0_txe1_led+b5_ee_ce_hw.elf urboot.c
```

