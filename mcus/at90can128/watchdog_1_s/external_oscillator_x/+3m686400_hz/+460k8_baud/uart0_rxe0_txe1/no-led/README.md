The AT90CAN128 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jPr--`|[urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90can128/watchdog_1_s/external_oscillator_x/%2B3m686400_hz/%2B460k8_baud/uart0_rxe0_txe1/no-led/urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90can128/watchdog_1_s/external_oscillator_x/%2B3m686400_hz/%2B460k8_baud/uart0_rxe0_txe1/no-led/urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr.hex)|
|368|512|u8.0|`w-U-jPr-c`|[urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90can128/watchdog_1_s/external_oscillator_x/%2B3m686400_hz/%2B460k8_baud/uart0_rxe0_txe1/no-led/urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr_ce.hex)|
|372|512|u8.0|`weU-jPr--`|[urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90can128/watchdog_1_s/external_oscillator_x/%2B3m686400_hz/%2B460k8_baud/uart0_rxe0_txe1/no-led/urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr_ee.hex)|
|424|512|u8.0|`weU-jPr-c`|[urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90can128/watchdog_1_s/external_oscillator_x/%2B3m686400_hz/%2B460k8_baud/uart0_rxe0_txe1/no-led/urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_pr_ee_ce.hex)|
|406|1024|u8.0|`weU-hpr-c`|[urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90can128/watchdog_1_s/external_oscillator_x/%2B3m686400_hz/%2B460k8_baud/uart0_rxe0_txe1/no-led/urboot_c128_1s_x3m6864_460k8_uart0_rxe0_txe1_no-led_ee_ce_hw.hex)|

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
  + `x3m6864` is F<sub>CPU</sub> of an external oscillator, here 3.6864 MHz
  + `460k8` shows the fixed communication baud rate, here 460800 baud
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
make MCU=at90can128 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led
make MCU=at90can128 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr
make MCU=at90can128 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr_ce
make MCU=at90can128 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr_ee
make MCU=at90can128 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr_ee_ce
make MCU=at90can128 WDTO=1S F_CPU=8000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf79 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=144 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf7b -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=140 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf95 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=88 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce95 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=618 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=8000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_x8m0_1000k0_uart0_rxe0_txe1_no-led_ee_ce_hw.elf urboot.c
```

