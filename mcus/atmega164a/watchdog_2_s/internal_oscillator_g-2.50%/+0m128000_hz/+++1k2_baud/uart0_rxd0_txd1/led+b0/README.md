The ATmega164A exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|242|256|u8.0|`w---hpr--`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0_hw.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0_pr.hex)|
|352|384|u8.0|`w-U-jPr-c`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0_pr_ce.hex)|
|362|384|u8.0|`weU-jPr--`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0_pr_ee.hex)|
|368|384|u8.0|`weU-jPr-c`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0_pr_ee_ce.hex)|
|390|512|u8.0|`weU-hpr-c`|[urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega164a/watchdog_2_s/internal_oscillator_g-2.50%25/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led%2Bb0/urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led%2Bb0_ee_ce_hw.hex)|

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
  + `g0m128` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.128 MHz - 2.50%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b0` toggles an active-high (`+`) LED on pin `B0`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_hw
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ce
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ee
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ee_ce
make MCU=atmega164a WDTO=2S F_CPU=124800L BAUD_RATE=1200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB0 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb3 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb8 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc5 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf8f -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=122 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega164a -DF_CPU=124800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1200 -DLED=AtmelPB0 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m164a_2s_g0m128_1k2_uart0_rxd0_txd1_led+b0_ee_ce_hw.elf urboot.c
```

