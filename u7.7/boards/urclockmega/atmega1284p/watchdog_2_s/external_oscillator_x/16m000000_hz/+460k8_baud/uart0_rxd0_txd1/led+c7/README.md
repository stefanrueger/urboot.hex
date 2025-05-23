The ATmega1284P exhibits a SWIO baud rate quantisation error of -0.79% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.79% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|296|512|u7.7|`w-u-jPr--`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7.hex)|
|296|512|u7.7|`w-u-jPr--`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7_pr.hex)|
|340|512|u7.7|`w-u-jPr-c`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7_pr_ce.hex)|
|358|512|u7.7|`weu-jPr--`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7_pr_ee.hex)|
|402|512|u7.7|`weu-jPr-c`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7_pr_ee_ce.hex)|
|384|1024|u7.7|`weu-hpr-c`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7_ee_ce_hw.hex)|
|490|1024|u7.7|`wes-hpr-c`|[urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led+c7_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/boards/urclockmega/atmega1284p/watchdog_2_s/external_oscillator_x/16m000000_hz/%2B460k8_baud/uart0_rxd0_txd1/led%2Bc7/urboot_m1284p_2s_x16m0_460k8_swio_rxd0_txd1_led%2Bc7_ee_ce_hw_stk500.hex)|

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
  + `x16m0` is F<sub>CPU</sub> of an external oscillator, here 16.0 MHz
  + `460k8` shows the fixed communication baud rate, here 460800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+c7` toggles an active-high (`+`) LED on pin `C7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr_ce
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr_ee
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr_ee_ce
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_ee_ce_hw
make MCU=atmega1284p WDTO=2S F_CPU=20000000L BAUD_RATE=576000 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPC7 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6b -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=234 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6b -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=216 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf81 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=172 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf8a -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=154 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa0 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=110 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcea0 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=640 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xced5 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=534 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=576000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x20m0_576k0_swio_rxd0_txd1_led+c7_ee_ce_hw_stk500.elf urboot.c
```

