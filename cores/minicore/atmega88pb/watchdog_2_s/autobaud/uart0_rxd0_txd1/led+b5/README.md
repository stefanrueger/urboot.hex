Note that autobaud bootloaders normally can only detect host baud rates = f/8, f/16, ... f/2048 +/- 1.5%, where f=F<sub>CPU</sub>. Internal oscillators have a high unknown deviation: baud rates under f/260 are recommended for these.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---hpra-`|[urboot_atmega88pb_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb_hw.hex)|
|256|256|u8.0|`w---jpra-`|[urboot_atmega88pb.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb.hex)|
|310|320|u8.0|`w---jPrac`|[urboot_atmega88pb_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb_pr_ce.hex)|
|320|320|u8.0|`w-U-jPra-`|[urboot_atmega88pb_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb_pr.hex)|
|322|384|u8.0|`we--jPra-`|[urboot_atmega88pb_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb_pr_ee.hex)|
|366|384|u8.0|`we--jPrac`|[urboot_atmega88pb_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb_pr_ee_ce.hex)|
|414|512|u8.0|`weU-hprac`|[urboot_atmega88pb_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega88pb/watchdog_2_s/autobaud/uart0_rxd0_txd1/led%2Bb5/urboot_atmega88pb_ee_ce_hw.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_hw
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr_ce
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr_ee
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr_ee_ce
make MCU=atmega88pb WDTO=2S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfc8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf9b -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=98 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega88pb -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m88pb_2s_autobaud_uart0_rxd0_txd1_led+b5_ee_ce_hw.elf urboot.c
```

