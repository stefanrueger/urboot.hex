The ATmega48 exhibits a SWIO baud rate quantisation error of -0.37% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.37% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jPr--`|[urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led%2Bb5.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led%2Bb5_pr.hex)|
|304|320|u8.0|`w---jPr-c`|[urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led%2Bb5_pr_ce.hex)|
|316|320|u8.0|`we--jPr--`|[urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led%2Bb5_pr_ee.hex)|
|382|384|u8.0|`weU-jPr-c`|[urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega48/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B125k0_baud/uart0_rxd0_txd1/led%2Bb5/urboot_m48_2s_x4m608_125k0_swio_rxd0_txd1_led%2Bb5_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x4m608` is F<sub>CPU</sub> of an external oscillator, here 4.608 MHz
  + `125k0` shows the fixed communication baud rate, here 125000 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=500000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=500000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=500000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr_ce
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=500000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr_ee
make MCU=atmega48 WDTO=2S F_CPU=18432000L BAUD_RATE=500000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=0 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd4 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfce -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega48 -DF_CPU=18432000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m48_2s_x18m432_500k0_swio_rxd0_txd1_led+b5_pr_ee_ce.elf urboot.c
```

