The ATtiny1634 exhibits a SWIO baud rate quantisation error of -0.35% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.35% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/internal_oscillator_d-6.25%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxb1_txb2/lednop/urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop.hex)|
|286|384|u7.7|`w-u-jPr--`|[urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/internal_oscillator_d-6.25%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxb1_txb2/lednop/urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr.hex)|
|312|384|u7.7|`w-u-jPr-c`|[urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/internal_oscillator_d-6.25%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxb1_txb2/lednop/urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr_ce.hex)|
|348|384|u7.7|`weu-jPr--`|[urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/internal_oscillator_d-6.25%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxb1_txb2/lednop/urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr_ee.hex)|
|374|384|u7.7|`weu-jPr-c`|[urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny1634/watchdog_2_s/internal_oscillator_d-6.25%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxb1_txb2/lednop/urboot_t1634_2s_d1m0_9k6_swio_rxb1_txb2_lednop_pr_ee_ce.hex)|

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
  + `d1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 5%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny1634 WDTO=2S F_CPU=7500000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop
make MCU=attiny1634 WDTO=2S F_CPU=7500000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr
make MCU=attiny1634 WDTO=2S F_CPU=7500000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr_ce
make MCU=attiny1634 WDTO=2S F_CPU=7500000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr_ee
make MCU=attiny1634 WDTO=2S F_CPU=7500000L BAUD_RATE=76800 SWIO=1 RX=AtmelPB1 TX=AtmelPB2 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdf -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcf9f -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=116 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfac -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=90 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfbe -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=6 -D_urboot_AVAILABLE=28 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny1634 -DF_CPU=7500000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB2 -DRX=AtmelPB1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t1634_2s_d8m0_76k8_swio_rxb1_txb2_lednop_pr_ee_ce.elf urboot.c
```

