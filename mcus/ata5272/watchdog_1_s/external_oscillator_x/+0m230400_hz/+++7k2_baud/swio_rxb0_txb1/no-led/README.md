The ATA5272 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jpr--`|[urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led.hex)|
|330|384|u8.0|`w-U-jPr--`|[urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr.hex)|
|364|384|u8.0|`we--jPr-c`|[urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|
|374|384|u8.0|`w-U-jPr-c`|[urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|376|384|u8.0|`weU-jPr--`|[urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/external_oscillator_x/%2B0m230400_hz/%2B%2B%2B7k2_baud/swio_rxb0_txb1/no-led/urboot_a5272_1s_x0m2304_7k2_swio_rxb0_txb1_no-led_pr_ee.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x0m2304` is F<sub>CPU</sub> of an external oscillator, here 0.2304 MHz
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5272 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led
make MCU=ata5272 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr
make MCU=ata5272 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr_ee_ce
make MCU=ata5272 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr_ce
make MCU=ata5272 WDTO=1S F_CPU=18432000L BAUD_RATE=576000 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr_ee
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe5 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfaa -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc0 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=18432000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=576000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_x18m432_576k0_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
```

