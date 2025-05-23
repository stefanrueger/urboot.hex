The ATtiny441 exhibits a SWIO baud rate quantisation error of +0.25% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.25% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---jpr--`|[urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart0_rxa2_txa1/lednop/urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop.hex)|
|286|320|u8.0|`w---jPr--`|[urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart0_rxa2_txa1/lednop/urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr.hex)|
|310|320|u8.0|`w---jPr-c`|[urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart0_rxa2_txa1/lednop/urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr_ce.hex)|
|320|320|u8.0|`we--jPr--`|[urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart0_rxa2_txa1/lednop/urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr_ee.hex)|
|362|384|u8.0|`we--jPr-c`|[urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart0_rxa2_txa1/lednop/urboot_t441_1s_k1m0_7k2_swio_rxa2_txa1_lednop_pr_ee_ce.hex)|

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
  + `k1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 2.50%
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny441 WDTO=1S F_CPU=8200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop
make MCU=attiny441 WDTO=1S F_CPU=8200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr
make MCU=attiny441 WDTO=1S F_CPU=8200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr_ce
make MCU=attiny441 WDTO=1S F_CPU=8200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr_ee
make MCU=attiny441 WDTO=1S F_CPU=8200000L BAUD_RATE=57600 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdf -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_1s_k8m0_57k6_swio_rxa2_txa1_lednop_pr_ee_ce.elf urboot.c
```

