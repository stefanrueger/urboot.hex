The ATA6285 exhibits a SWIO baud rate quantisation error of -0.18% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.18% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---hpr--`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_hw.hex)|
|256|256|u8.0|`w---jpr--`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led.hex)|
|310|320|u8.0|`w---jPr-c`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ce.hex)|
|320|320|u8.0|`w-U-jPr--`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr.hex)|
|322|384|u8.0|`we--jPr--`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee.hex)|
|366|384|u8.0|`we--jPr-c`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|
|414|512|u8.0|`weU-hpr-c`|[urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6285/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B1m000000_hz/%2B%2B%2B1k2_baud/swio_rxb0_txb1/no-led/urboot_a6285_2s_n1m0_1k2_swio_rxb0_txb1_no-led_ee_ce_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `n1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 6.25%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_hw
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr_ce
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr_ee
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr_ee_ce
make MCU=ata6285 WDTO=2S F_CPU=4250000L BAUD_RATE=4800 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf9b -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=98 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6285 -DF_CPU=4250000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6285_2s_n4m0_4k8_swio_rxb0_txb1_no-led_ee_ce_hw.elf urboot.c
```

