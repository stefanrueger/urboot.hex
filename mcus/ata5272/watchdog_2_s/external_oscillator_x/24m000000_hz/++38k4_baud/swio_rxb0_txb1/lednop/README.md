The ATA5272 exhibits a SWIO baud rate quantisation error of +0.32% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.32% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_2_s/external_oscillator_x/24m000000_hz/%2B%2B38k4_baud/swio_rxb0_txb1/lednop/urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop.hex)|
|290|384|u7.7|`w-u-jPr--`|[urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_2_s/external_oscillator_x/24m000000_hz/%2B%2B38k4_baud/swio_rxb0_txb1/lednop/urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr.hex)|
|316|384|u7.7|`w-u-jPr-c`|[urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_2_s/external_oscillator_x/24m000000_hz/%2B%2B38k4_baud/swio_rxb0_txb1/lednop/urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ce.hex)|
|352|384|u7.7|`weu-jPr--`|[urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_2_s/external_oscillator_x/24m000000_hz/%2B%2B38k4_baud/swio_rxb0_txb1/lednop/urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee.hex)|
|378|384|u7.7|`weu-jPr-c`|[urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5272/watchdog_2_s/external_oscillator_x/24m000000_hz/%2B%2B38k4_baud/swio_rxb0_txb1/lednop/urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|

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
  + `x24m0` is F<sub>CPU</sub> of an external oscillator, here 24.0 MHz
  + `38k4` shows the fixed communication baud rate, here 38400 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5272 WDTO=2S F_CPU=24000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop
make MCU=ata5272 WDTO=2S F_CPU=24000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr
make MCU=ata5272 WDTO=2S F_CPU=24000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ce
make MCU=ata5272 WDTO=2S F_CPU=24000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee
make MCU=ata5272 WDTO=2S F_CPU=24000000L BAUD_RATE=38400 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=2 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfa4 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=112 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=86 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc3 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=50 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5272 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=38400 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5272_2s_x24m0_38k4_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
```

