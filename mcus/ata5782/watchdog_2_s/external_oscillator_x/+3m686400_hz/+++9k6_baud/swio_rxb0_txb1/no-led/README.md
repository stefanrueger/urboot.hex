The ATA5782 exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jpr--`|[urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5782/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led.hex)|
|256|256|u8.0|`w---jpr--`|[urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5782/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr.hex)|
|318|320|u8.0|`we--jpr--`|[urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5782/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr_ee.hex)|
|320|320|u8.0|`w-U-jpr-c`|[urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5782/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr_ce.hex)|
|376|384|u8.0|`weU-jpr-c`|[urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5782/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_pr_ee_ce.hex)|
|366|20464|u8.0|`-eU-hpr-c`|[urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5782/watchdog_2_s/external_oscillator_x/%2B3m686400_hz/%2B%2B%2B9k6_baud/swio_rxb0_txb1/no-led/urboot_a5782_2s_x3m6864_9k6_swio_rxb0_txb1_no-led_ee_ce_hw.hex)|

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
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x3m6864` is F<sub>CPU</sub> of an external oscillator, here 3.6864 MHz
  + `9k6` shows the fixed communication baud rate, here 9600 baud
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
make MCU=ata5782 WDTO=2S F_CPU=22118400L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led
make MCU=ata5782 WDTO=2S F_CPU=22118400L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr
make MCU=ata5782 WDTO=2S F_CPU=22118400L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr_ee
make MCU=ata5782 WDTO=2S F_CPU=22118400L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr_ce
make MCU=ata5782 WDTO=2S F_CPU=22118400L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr_ee_ce
make MCU=ata5782 WDTO=2S F_CPU=22118400L BAUD_RATE=57600 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 PGMWRITEPAGE=0 NAME=urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4f00UL -DRJMPWP=0xcfe5 -Wl,--section-start=.text=0x4f00 -Wl,--section-start=.version=0x4ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5782 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4f00UL -DRJMPWP=0xcfe5 -Wl,--section-start=.text=0x4f00 -Wl,--section-start=.version=0x4ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5782 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4ec0UL -DRJMPWP=0xcfe2 -Wl,--section-start=.text=0x4ec0 -Wl,--section-start=.version=0x4ffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5782 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4ec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x4ec0 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5782 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4e80UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x4e80 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5782 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x0UL -DRJMPWP=0x9508 -Wl,--section-start=.text=0x0 -Wl,--section-start=.version=0x4ffa -DFRILLS=10 -D_urboot_AVAILABLE=20098 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5782 -DF_CPU=22118400L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5782_2s_x22m1184_57k6_swio_rxb0_txb1_no-led_ee_ce_hw.elf urboot.c
```

