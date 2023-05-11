The ATA5505 exhibits a LINUART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u7.7|`w-u-jPr--`|[urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5505/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B125k0_baud/uart0_rxa0_txa1/no-led/urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5505/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B125k0_baud/uart0_rxa0_txa1/no-led/urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr.hex)|
|280|384|u7.7|`w-u-jPr-c`|[urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5505/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B125k0_baud/uart0_rxa0_txa1/no-led/urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr_ce.hex)|
|316|384|u7.7|`weu-jPr--`|[urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5505/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B125k0_baud/uart0_rxa0_txa1/no-led/urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr_ee.hex)|
|342|384|u7.7|`weu-jPr-c`|[urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5505/watchdog_1_s/external_oscillator_x/10m000000_hz/%2B125k0_baud/uart0_rxa0_txa1/no-led/urboot_a5505_1s_x10m0_125k0_uart0_rxa0_txa1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x10m0` is F<sub>CPU</sub> of an external oscillator, here 10.0 MHz
  + `125k0` shows the fixed communication baud rate, here 125000 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5505 WDTO=1S F_CPU=20000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led
make MCU=ata5505 WDTO=1S F_CPU=20000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr
make MCU=ata5505 WDTO=1S F_CPU=20000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr_ce
make MCU=ata5505 WDTO=1S F_CPU=20000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr_ee
make MCU=ata5505 WDTO=1S F_CPU=20000000L BAUD_RATE=250000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5505 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5505 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfa8 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=104 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5505 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfba -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=68 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5505 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=42 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5505 -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DBAUD_RATE=250000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5505_1s_x20m0_250k0_uart0_rxa0_txa1_no-led_pr_ee_ce.elf urboot.c
```

