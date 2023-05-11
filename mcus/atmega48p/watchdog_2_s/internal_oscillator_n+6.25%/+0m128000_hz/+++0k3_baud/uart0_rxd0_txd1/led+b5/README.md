The ATmega48P exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u7.7|`w-u-jpr--`|[urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led%2Bb5.hex)|
|288|320|u7.7|`w-u-jPr--`|[urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led%2Bb5_pr.hex)|
|314|320|u7.7|`w-u-jPr-c`|[urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led%2Bb5_pr_ce.hex)|
|346|384|u7.7|`weu-jPr--`|[urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led%2Bb5_pr_ee.hex)|
|372|384|u7.7|`weu-jPr-c`|[urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48p/watchdog_2_s/internal_oscillator_n%2B6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led%2Bb5_pr_ee_ce.hex)|

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
  + `n0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 6.25%
  + `0k3` shows the fixed communication baud rate, here 300 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega48p WDTO=2S F_CPU=136000L BAUD_RATE=300 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5
make MCU=atmega48p WDTO=2S F_CPU=136000L BAUD_RATE=300 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr
make MCU=atmega48p WDTO=2S F_CPU=136000L BAUD_RATE=300 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ce
make MCU=atmega48p WDTO=2S F_CPU=136000L BAUD_RATE=300 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ee
make MCU=atmega48p WDTO=2S F_CPU=136000L BAUD_RATE=300 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=136000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=136000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=136000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=136000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48p -DF_CPU=136000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=300 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48p_2s_n0m128_0k3_swio_rxd0_txd1_led+b5_pr_ee_ce.elf urboot.c
```

