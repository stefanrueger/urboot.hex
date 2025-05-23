The ATtiny2313 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|192|192|u8.0|`w---jpr--`|[urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B230k4_baud/uart0_rxd0_txd1/no-led/urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led.hex)|
|216|224|u8.0|`w---jPr--`|[urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B230k4_baud/uart0_rxd0_txd1/no-led/urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr.hex)|
|244|256|u8.0|`w---jPr-c`|[urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B230k4_baud/uart0_rxd0_txd1/no-led/urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr_ce.hex)|
|282|288|u8.0|`we--jPr--`|[urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B230k4_baud/uart0_rxd0_txd1/no-led/urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr_ee.hex)|
|288|288|u8.0|`we--jPr-c`|[urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_1_s/external_oscillator_x/%2B7m372800_hz/%2B230k4_baud/uart0_rxd0_txd1/no-led/urboot_t2313_1s_x7m3728_230k4_uart0_rxd0_txd1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x7m3728` is F<sub>CPU</sub> of an external oscillator, here 7.3728 MHz
  + `230k4` shows the fixed communication baud rate, here 230400 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny2313 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led
make MCU=attiny2313 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr
make MCU=attiny2313 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr_ce
make MCU=attiny2313 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr_ee
make MCU=attiny2313 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x740UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x740 -Wl,--section-start=.version=0x7fa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=4 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x700UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x700 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x6e0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x6e0 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x6e0UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x6e0 -Wl,--section-start=.version=0x7fa -DFRILLS=2 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_1s_x18m432_576k0_uart0_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
```

