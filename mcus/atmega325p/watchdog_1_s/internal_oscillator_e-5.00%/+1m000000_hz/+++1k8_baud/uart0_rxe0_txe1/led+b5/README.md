The ATmega325P exhibits a UART baud rate quantisation error of -0.04% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.04% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jPr--`|[urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega325p/watchdog_1_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B1k8_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led%2Bb5.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega325p/watchdog_1_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B1k8_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led%2Bb5_pr.hex)|
|356|384|u8.0|`w-U-jPr-c`|[urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega325p/watchdog_1_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B1k8_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led%2Bb5_pr_ce.hex)|
|366|384|u8.0|`weU-jPr--`|[urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega325p/watchdog_1_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B1k8_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led%2Bb5_pr_ee.hex)|
|372|384|u8.0|`weU-jPr-c`|[urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega325p/watchdog_1_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B1k8_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led%2Bb5_pr_ee_ce.hex)|
|394|512|u8.0|`weU-hpr-c`|[urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega325p/watchdog_1_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B1k8_baud/uart0_rxe0_txe1/led%2Bb5/urboot_m325p_1s_e1m0_1k8_uart0_rxe0_txe1_led%2Bb5_ee_ce_hw.hex)|

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
  + `e1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 5.00%
  + `1k8` shows the fixed communication baud rate, here 1800 baud
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
make MCU=atmega325p WDTO=1S F_CPU=7600000L BAUD_RATE=14400 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5
make MCU=atmega325p WDTO=1S F_CPU=7600000L BAUD_RATE=14400 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr
make MCU=atmega325p WDTO=1S F_CPU=7600000L BAUD_RATE=14400 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr_ce
make MCU=atmega325p WDTO=1S F_CPU=7600000L BAUD_RATE=14400 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr_ee
make MCU=atmega325p WDTO=1S F_CPU=7600000L BAUD_RATE=14400 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr_ee_ce
make MCU=atmega325p WDTO=1S F_CPU=7600000L BAUD_RATE=14400 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega325p -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega325p -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb5 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega325p -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfba -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega325p -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega325p -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf91 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=118 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega325p -DF_CPU=7600000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m325p_1s_e8m0_14k4_uart0_rxe0_txe1_led+b5_ee_ce_hw.elf urboot.c
```

