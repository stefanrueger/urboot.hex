The ATtiny841 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---jPr--`|[urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/uart1_rxa4_txa5/no-led/urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led.hex)|
|246|256|u8.0|`w---jPr--`|[urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/uart1_rxa4_txa5/no-led/urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr.hex)|
|254|256|u8.0|`w---jPr-c`|[urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/uart1_rxa4_txa5/no-led/urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr_ce.hex)|
|306|320|u8.0|`we--jPr--`|[urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/uart1_rxa4_txa5/no-led/urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr_ee.hex)|
|316|320|u8.0|`we--jPr-c`|[urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_1_s/external_oscillator_x/%2B8m000000_hz/%2B250k0_baud/uart1_rxa4_txa5/no-led/urboot_t841_1s_x8m0_250k0_uart1_rxa4_txa5_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x8m0` is F<sub>CPU</sub> of an external oscillator, here 8.0 MHz
  + `250k0` shows the fixed communication baud rate, here 250000 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny841 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led
make MCU=attiny841 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr
make MCU=attiny841 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr_ce
make MCU=attiny841 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr_ee
make MCU=attiny841 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_1s_x18m432_576k0_uart1_rxa4_txa5_no-led_pr_ee_ce.elf urboot.c
```

