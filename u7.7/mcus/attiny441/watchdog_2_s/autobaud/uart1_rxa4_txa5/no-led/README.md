Note that autobaud bootloaders normally can only detect host baud rates = f/8, f/16, ... f/2048 +/- 1.5%, where f=F<sub>CPU</sub>. Internal oscillators have a high unknown deviation: baud rates under f/260 are recommended for these.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jPra-`|[urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_2_s/autobaud/uart1_rxa4_txa5/no-led/urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led.hex)|
|256|256|u7.7|`w-u-jPra-`|[urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_2_s/autobaud/uart1_rxa4_txa5/no-led/urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr.hex)|
|300|320|u7.7|`w-u-jPrac`|[urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_2_s/autobaud/uart1_rxa4_txa5/no-led/urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ce.hex)|
|320|320|u7.7|`weu-jPra-`|[urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_2_s/autobaud/uart1_rxa4_txa5/no-led/urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee.hex)|
|362|384|u7.7|`weu-jPrac`|[urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/attiny441/watchdog_2_s/autobaud/uart1_rxa4_txa5/no-led/urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee_ce.hex)|

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
  + `a` autobaud detection (f_cpu/8n using discrete divisors, n = 1, 2, ..., 256)
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `autobaud` detects host baud rate f/8, f/16, f/24, ..., f/2048 (f=F<sub>CPU</sub>)
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny441 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led
make MCU=attiny441 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr
make MCU=attiny441 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ce
make MCU=attiny441 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee
make MCU=attiny441 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfcf -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=2 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_autobaud_uart1_rxa4_txa5_no-led_pr_ee_ce.elf urboot.c
```

