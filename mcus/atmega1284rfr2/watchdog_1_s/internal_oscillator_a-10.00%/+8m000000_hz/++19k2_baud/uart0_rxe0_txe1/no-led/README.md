The ATmega1284RFR2 exhibits a UART baud rate quantisation error of -0.27% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.27% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jPr--`|[urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284rfr2/watchdog_1_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/no-led/urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led.hex)|
|254|256|u8.0|`w---jPr--`|[urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284rfr2/watchdog_1_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/no-led/urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr.hex)|
|360|512|u8.0|`w-U-jPr-c`|[urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284rfr2/watchdog_1_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/no-led/urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ce.hex)|
|364|512|u8.0|`weU-jPr--`|[urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284rfr2/watchdog_1_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/no-led/urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee.hex)|
|416|512|u8.0|`weU-jPr-c`|[urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284rfr2/watchdog_1_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/no-led/urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee_ce.hex)|
|398|1024|u8.0|`weU-hpr-c`|[urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284rfr2/watchdog_1_s/internal_oscillator_a-10.00%25/%2B8m000000_hz/%2B%2B19k2_baud/uart0_rxe0_txe1/no-led/urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_ee_ce_hw.hex)|

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
  + `a8m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 8.0 MHz - 10.00%
  + `19k2` shows the fixed communication baud rate, here 19200 baud
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
make MCU=atmega1284rfr2 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led
make MCU=atmega1284rfr2 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr
make MCU=atmega1284rfr2 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ce
make MCU=atmega1284rfr2 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee
make MCU=atmega1284rfr2 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee_ce
make MCU=atmega1284rfr2 WDTO=1S F_CPU=7200000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284rfr2 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284rfr2 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf75 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=152 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284rfr2 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf77 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=148 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284rfr2 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf91 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=96 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284rfr2 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce91 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=626 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284rfr2 -DF_CPU=7200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284rfr2_1s_a8m0_19k2_uart0_rxe0_txe1_no-led_ee_ce_hw.elf urboot.c
```

