The ATtiny441 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jpr--`|[urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_d-6.25%25/%2B0m256000_hz/%2B%2B%2B2k4_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop.hex)|
|286|320|u8.0|`w---jPr--`|[urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_d-6.25%25/%2B0m256000_hz/%2B%2B%2B2k4_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr.hex)|
|310|320|u8.0|`w---jPr-c`|[urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_d-6.25%25/%2B0m256000_hz/%2B%2B%2B2k4_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr_ce.hex)|
|320|320|u8.0|`we--jPr--`|[urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_d-6.25%25/%2B0m256000_hz/%2B%2B%2B2k4_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr_ee.hex)|
|362|384|u8.0|`we--jPr-c`|[urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_d-6.25%25/%2B0m256000_hz/%2B%2B%2B2k4_baud/uart1_rxa4_txa5/lednop/urboot_t441_1s_d0m256_2k4_swio_rxa4_txa5_lednop_pr_ee_ce.hex)|

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
  + `d0m256` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.256 MHz - 6.25%
  + `2k4` shows the fixed communication baud rate, here 2400 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny441 WDTO=1S F_CPU=480000L BAUD_RATE=4800 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop
make MCU=attiny441 WDTO=1S F_CPU=480000L BAUD_RATE=4800 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr
make MCU=attiny441 WDTO=1S F_CPU=480000L BAUD_RATE=4800 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr_ce
make MCU=attiny441 WDTO=1S F_CPU=480000L BAUD_RATE=4800 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr_ee
make MCU=attiny441 WDTO=1S F_CPU=480000L BAUD_RATE=4800 SWIO=1 RX=AtmelPA4 TX=AtmelPA5 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdf -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=480000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=480000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=480000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=480000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=480000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA5 -DRX=AtmelPA4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_d0m512_4k8_swio_rxa4_txa5_lednop_pr_ee_ce.elf urboot.c
```

