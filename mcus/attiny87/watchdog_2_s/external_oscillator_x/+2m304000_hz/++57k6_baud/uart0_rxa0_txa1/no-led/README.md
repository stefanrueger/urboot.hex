The ATtiny87 exhibits a LINUART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---jPr--`|[urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_2_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart0_rxa0_txa1/no-led/urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led.hex)|
|246|256|u8.0|`w---jPr--`|[urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_2_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart0_rxa0_txa1/no-led/urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr.hex)|
|254|256|u8.0|`w---jPr-c`|[urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_2_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart0_rxa0_txa1/no-led/urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr_ce.hex)|
|352|384|u8.0|`weU-jPr--`|[urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_2_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart0_rxa0_txa1/no-led/urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr_ee.hex)|
|376|384|u8.0|`weU-jPr-c`|[urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny87/watchdog_2_s/external_oscillator_x/%2B2m304000_hz/%2B%2B57k6_baud/uart0_rxa0_txa1/no-led/urboot_t87_2s_x2m304_57k6_uart0_rxa0_txa1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x2m304` is F<sub>CPU</sub> of an external oscillator, here 2.304 MHz
  + `57k6` shows the fixed communication baud rate, here 57600 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny87 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led
make MCU=attiny87 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr
make MCU=attiny87 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr_ce
make MCU=attiny87 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr_ee
make MCU=attiny87 WDTO=2S F_CPU=20000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb5 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny87 -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t87_2s_x20m0_500k0_uart0_rxa0_txa1_no-led_pr_ee_ce.elf urboot.c
```

