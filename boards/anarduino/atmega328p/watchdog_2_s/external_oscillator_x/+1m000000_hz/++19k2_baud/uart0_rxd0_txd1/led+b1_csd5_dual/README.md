The ATmega328P exhibits a SWIO baud rate quantisation error of +0.16% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.16% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|472|512|u8.1|`w-UdjPr--`|[urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led+b1_csd5_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/anarduino/atmega328p/watchdog_2_s/external_oscillator_x/%2B1m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led%2Bb1_csd5_dual.hex)|
|472|512|u8.1|`w-UdjPr--`|[urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led+b1_csd5_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/anarduino/atmega328p/watchdog_2_s/external_oscillator_x/%2B1m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led%2Bb1_csd5_dual_pr.hex)|
|496|512|u8.1|`we-dhpr-c`|[urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/anarduino/atmega328p/watchdog_2_s/external_oscillator_x/%2B1m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led%2Bb1_csd5_dual_ee_ce_hw.hex)|
|508|512|u8.1|`w-UdjPr-c`|[urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led+b1_csd5_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/anarduino/atmega328p/watchdog_2_s/external_oscillator_x/%2B1m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led%2Bb1_csd5_dual_pr_ce.hex)|
|508|512|u8.1|`weUdjPr--`|[urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led+b1_csd5_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/anarduino/atmega328p/watchdog_2_s/external_oscillator_x/%2B1m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led%2Bb1_csd5_dual_pr_ee.hex)|
|510|512|u8.1|`we-djPr-c`|[urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/anarduino/atmega328p/watchdog_2_s/external_oscillator_x/%2B1m000000_hz/%2B%2B19k2_baud/uart0_rxd0_txd1/led%2Bb1_csd5_dual/urboot_m328p_2s_x1m0_19k2_swio_rxd0_txd1_led%2Bb1_csd5_dual_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
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
  + `x1m0` is F<sub>CPU</sub> of an external oscillator, here 1.0 MHz
  + `19k2` shows the fixed communication baud rate, here 19200 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b1` toggles an active-high (`+`) LED on pin `B1`
  + `csd5` uses pin D5 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=2S F_CPU=24000000L BAUD_RATE=460800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual
make MCU=atmega328p WDTO=2S F_CPU=24000000L BAUD_RATE=460800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr
make MCU=atmega328p WDTO=2S F_CPU=24000000L BAUD_RATE=460800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw
make MCU=atmega328p WDTO=2S F_CPU=24000000L BAUD_RATE=460800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=24000000L BAUD_RATE=460800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=24000000L BAUD_RATE=460800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB1 SFMCS=AtmelPD5 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=460800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfb1 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=40 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=460800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=460800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=9 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=460800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=460800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=460800 -DLED=AtmelPB1 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPD5 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x24m0_460k8_swio_rxd0_txd1_led+b1_csd5_dual_pr_ee_ce.elf urboot.c
```

