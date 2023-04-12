The ATtiny441 exhibits a SWIO baud rate quantisation error of +0.64% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.64% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/external_oscillator_x/%2B2m000000_hz/%2B%2B28k8_baud/uart1_rxa4_txa5/no-led/urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led.hex)|
|282|320|u7.7|`w-u-jPr--`|[urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/external_oscillator_x/%2B2m000000_hz/%2B%2B28k8_baud/uart1_rxa4_txa5/no-led/urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr.hex)|
|308|320|u7.7|`w-u-jPr-c`|[urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/external_oscillator_x/%2B2m000000_hz/%2B%2B28k8_baud/uart1_rxa4_txa5/no-led/urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr_ce.hex)|
|344|384|u7.7|`weu-jPr--`|[urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/external_oscillator_x/%2B2m000000_hz/%2B%2B28k8_baud/uart1_rxa4_txa5/no-led/urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr_ee.hex)|
|370|384|u7.7|`weu-jPr-c`|[urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/external_oscillator_x/%2B2m000000_hz/%2B%2B28k8_baud/uart1_rxa4_txa5/no-led/urboot_t441_2s_x2m0_28k8_swio_rxa4_txa5_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x2m0` is F<sub>CPU</sub> of an external oscillator, here 2.0 MHz
  + `28k8` shows the fixed communication baud rate, here 28800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny441 WDTO=2S F_CPU=16000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led
make MCU=attiny441 WDTO=2S F_CPU=16000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr
make MCU=attiny441 WDTO=2S F_CPU=16000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr_ce
make MCU=attiny441 WDTO=2S F_CPU=16000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr_ee
make MCU=attiny441 WDTO=2S F_CPU=16000000L BAUD_RATE=230400 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=4 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=230400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfbd -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=56 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=230400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=230400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfbc -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=230400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=230400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_x16m0_230k4_swio_rxa4_txa5_no-led_pr_ee_ce.elf urboot.c
```

