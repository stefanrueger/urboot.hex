Note that autobaud bootloaders normally can only detect host baud rates = f/8, f/16, ... f/2048 +/- 1.5%, where f=F<sub>CPU</sub>. Internal oscillators have a high unknown deviation: baud rates under f/260 are recommended for these.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jpra-`|[urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1280/watchdog_2_s/autobaud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led%2Bb7.hex)|
|330|512|u8.0|`w-U-jPra-`|[urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1280/watchdog_2_s/autobaud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led%2Bb7_pr.hex)|
|382|512|u8.0|`w-U-jPrac`|[urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1280/watchdog_2_s/autobaud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led%2Bb7_pr_ce.hex)|
|386|512|u8.0|`weU-jPra-`|[urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1280/watchdog_2_s/autobaud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led%2Bb7_pr_ee.hex)|
|438|512|u8.0|`weU-jPrac`|[urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1280/watchdog_2_s/autobaud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led%2Bb7_pr_ee_ce.hex)|
|420|1024|u8.0|`weU-hprac`|[urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1280/watchdog_2_s/autobaud/uart1_rxd2_txd3/led%2Bb7/urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led%2Bb7_ee_ce_hw.hex)|

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
  + `a` autobaud detection (f_cpu/8n using discrete divisors, n = 1, 2, ..., 256)
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `autobaud` detects host baud rate f/8, f/16, f/24, ..., f/2048 (f=F<sub>CPU</sub>)
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b7` toggles an active-high (`+`) LED on pin `B7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1280 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7
make MCU=atmega1280 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr
make MCU=atmega1280 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ce
make MCU=atmega1280 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ee
make MCU=atmega1280 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ee_ce
make MCU=atmega1280 WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf66 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=182 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf80 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=130 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf82 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=126 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf9c -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=74 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce9c -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=604 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_autobaud_uart1_rxd2_txd3_led+b7_ee_ce_hw.elf urboot.c
```

