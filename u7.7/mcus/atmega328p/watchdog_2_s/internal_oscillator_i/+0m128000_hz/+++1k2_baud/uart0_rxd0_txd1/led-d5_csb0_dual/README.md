The ATmega328P exhibits a SWIO baud rate quantisation error of -0.33% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.33% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|424|512|u7.7|`w-udjPr--`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual.hex)|
|424|512|u7.7|`w-udjPr--`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr.hex)|
|450|512|u7.7|`w-udjPr-c`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ce.hex)|
|490|512|u7.7|`weudjPr--`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee.hex)|
|502|512|u7.7|`weudhpr-c`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw.hex)|
|508|512|u7.7|`weudjPr-c`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee_ce.hex)|
|606|1024|u7.7|`wesdhpr-c`|[urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega328p/watchdog_2_s/internal_oscillator_i/%2B0m128000_hz/%2B%2B%2B1k2_baud/uart0_rxd0_txd1/led-d5_csb0_dual/urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `d` dual boot (over-the-air programming from external SPI flash)
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `i0m128` is F<sub>CPU</sub> of an internal oscillator, here 0.128 MHz
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led-d5` toggles an active-low (`-`) LED on pin `D5`
  + `csb0` uses pin B0 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee_ce
make MCU=atmega328p WDTO=2S F_CPU=128000L BAUD_RATE=1200 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LEDPOLARITY=-1 LED=AtmelPD5 SFMCS=AtmelPB0 DUAL=1 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=102 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=88 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfba -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=62 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x7c00UL -DRJMPWP=0xcf0f -Wl,--section-start=.text=0x7c00 -Wl,--section-start=.version=0x7ffa -DFRILLS=6 -D_urboot_AVAILABLE=418 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=128000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=1200 -DLED=AtmelPD5 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_i0m128_1k2_swio_rxd0_txd1_led-d5_csb0_dual_ee_ce_hw_stk500.elf urboot.c
```

