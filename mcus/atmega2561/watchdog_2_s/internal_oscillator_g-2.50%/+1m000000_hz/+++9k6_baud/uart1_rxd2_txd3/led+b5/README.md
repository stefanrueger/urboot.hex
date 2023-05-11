The ATmega2561 exhibits a SWIO baud rate quantisation error of -0.43% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.43% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|300|512|u7.7|`w-u-jPr--`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5.hex)|
|300|512|u7.7|`w-u-jPr--`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5_pr.hex)|
|344|512|u7.7|`w-u-jPr-c`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5_pr_ce.hex)|
|362|512|u7.7|`weu-jPr--`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5_pr_ee.hex)|
|406|512|u7.7|`weu-jPr-c`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5_pr_ee_ce.hex)|
|388|1024|u7.7|`weu-hpr-c`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5_ee_ce_hw.hex)|
|504|1024|u7.7|`wes-hpr-c`|[urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led+b5_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega2561/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B9k6_baud/uart1_rxd2_txd3/led%2Bb5/urboot_m2561_2s_g1m0_9k6_swio_rxd2_txd3_led%2Bb5_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `g1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 2.50%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b5` toggles an active-high (`+`) LED on pin `B5`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr_ce
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr_ee
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr_ee_ce
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_ee_ce_hw
make MCU=atmega2561 WDTO=2S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=230 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf6d -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=212 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf83 -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=168 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcf8c -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=150 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3fe00UL -DRJMPWP=0xcfa2 -Wl,--section-start=.text=0x3fe00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=106 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3fc00UL -DRJMPWP=0xcea2 -Wl,--section-start=.text=0x3fc00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=636 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x3fc00UL -DRJMPWP=0xcedc -Wl,--section-start=.text=0x3fc00 -Wl,--section-start=.version=0x3fffa -DFRILLS=6 -D_urboot_AVAILABLE=520 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega2561 -DF_CPU=7800000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=76800 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -Wl,--relax -nostartfiles -nostdlib -o urboot_m2561_2s_g8m0_76k8_swio_rxd2_txd3_led+b5_ee_ce_hw_stk500.elf urboot.c
```

