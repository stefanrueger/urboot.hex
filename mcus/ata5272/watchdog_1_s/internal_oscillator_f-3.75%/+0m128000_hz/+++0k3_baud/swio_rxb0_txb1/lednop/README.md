The ATA5272 exhibits a SWIO baud rate quantisation error of -0.08% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.08% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jpr--`|[urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxb0_txb1/lednop/urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop.hex)|
|334|384|u8.0|`w-U-jPr--`|[urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxb0_txb1/lednop/urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr.hex)|
|368|384|u8.0|`we--jPr-c`|[urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxb0_txb1/lednop/urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|
|378|384|u8.0|`w-U-jPr-c`|[urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxb0_txb1/lednop/urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ce.hex)|
|380|384|u8.0|`weU-jPr--`|[urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_1_s/internal_oscillator_f-3.75%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/swio_rxb0_txb1/lednop/urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee.hex)|

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
  + `f0m128` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.128 MHz - 3.75%
  + `0k3` shows the fixed communication baud rate, here 300 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5272 WDTO=1S F_CPU=123200L BAUD_RATE=300 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop
make MCU=ata5272 WDTO=1S F_CPU=123200L BAUD_RATE=300 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr
make MCU=ata5272 WDTO=1S F_CPU=123200L BAUD_RATE=300 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee_ce
make MCU=ata5272 WDTO=1S F_CPU=123200L BAUD_RATE=300 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ce
make MCU=ata5272 WDTO=1S F_CPU=123200L BAUD_RATE=300 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=123200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfac -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=50 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=123200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=123200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc2 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=123200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=123200L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=300 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_1s_f0m128_0k3_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
```

