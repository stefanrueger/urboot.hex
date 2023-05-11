Note that autobaud bootloaders normally can only detect host baud rates = f/8, f/16, ... f/2048 +/- 1.5%, where f=F<sub>CPU</sub>. Internal oscillators have a high unknown deviation: baud rates under f/260 are recommended for these.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|298|512|u7.7|`w-u-jPra-`|[urboot_at90can128.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128.hex)|
|298|512|u7.7|`w-u-jPra-`|[urboot_at90can128_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr.hex)|
|342|512|u7.7|`w-u-jPrac`|[urboot_at90can128_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr_ce.hex)|
|358|512|u7.7|`weu-jPra-`|[urboot_at90can128_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr_ee.hex)|
|402|512|u7.7|`weu-jPrac`|[urboot_at90can128_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_pr_ee_ce.hex)|
|384|1024|u7.7|`weu-hprac`|[urboot_at90can128_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_ee_ce_hw.hex)|
|490|1024|u7.7|`wes-hprac`|[urboot_at90can128_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can128/watchdog_1_s/autobaud/uart0_rxe0_txe1/led%2Bb5/urboot_at90can128_ee_ce_hw_stk500.hex)|

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
  + `a` autobaud detection (f_cpu/8n using discrete divisors, n = 1, 2, ..., 256)
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr_ce
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr_ee
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr_ee_ce
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_ee_ce_hw
make MCU=at90can128 WDTO=1S F_CPU=16000000L AUTOBAUD=1 UARTNUM=0 RX=AtmelPE0 TX=AtmelPE1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,4,3,2 NAME=urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6c -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=232 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf6c -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=214 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf82 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=170 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf8a -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=154 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfa0 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=110 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcea0 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=640 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xced5 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=534 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can128 -DF_CPU=16000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=1 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPE1 -DRX=AtmelPE0 -Wl,--relax -nostartfiles -nostdlib -o urboot_c128_1s_autobaud_uart0_rxe0_txe1_led+b5_ee_ce_hw_stk500.elf urboot.c
```

