The ATmega162 exhibits a SWIO baud rate quantisation error of -0.24% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.24% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---hpr--`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_hw.hex)|
|256|256|u8.0|`w---jpr--`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led.hex)|
|330|384|u8.0|`w-U-jPr--`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr.hex)|
|366|384|u8.0|`we--jPr-c`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr_ee_ce.hex)|
|376|384|u8.0|`w-U-jPr-c`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr_ce.hex)|
|376|384|u8.0|`weU-jPr--`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_pr_ee.hex)|
|414|512|u8.0|`weU-hpr-c`|[urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega162/watchdog_2_s/internal_oscillator_f-3.75%25/%2B1m000000_hz/%2B%2B%2B7k2_baud/uart1_rxb2_txb3/no-led/urboot_m162_2s_f1m0_7k2_swio_rxb2_txb3_no-led_ee_ce_hw.hex)|

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
  + `f1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 3.75%
  + `7k2` shows the fixed communication baud rate, here 7200 baud
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
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=0 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_hw
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr_ee_ce
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr_ce
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr_ee
make MCU=atmega162 WDTO=2S F_CPU=7700000L BAUD_RATE=57600 SWIO=1 RX=AtmelPB2 TX=AtmelPB3 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfa8 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=9 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e00UL -DRJMPWP=0xcf9b -Wl,--section-start=.text=0x3e00 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=98 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega162 -DF_CPU=7700000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB3 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m162_2s_f8m0_57k6_swio_rxb2_txb3_no-led_ee_ce_hw.elf urboot.c
```

