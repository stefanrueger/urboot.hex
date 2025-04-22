The ATmega1284P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|466|512|u8.1|`w-UdjPr--`|[urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led+c7_csb3_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_1_s/external_oscillator_x/%2B4m608000_hz/%2B%2B28k8_baud/uart0_rxd0_txd1/led%2Bc7_csb3_dual/urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led%2Bc7_csb3_dual.hex)|
|466|512|u8.1|`w-UdjPr--`|[urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led+c7_csb3_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_1_s/external_oscillator_x/%2B4m608000_hz/%2B%2B28k8_baud/uart0_rxd0_txd1/led%2Bc7_csb3_dual/urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led%2Bc7_csb3_dual_pr.hex)|
|508|512|u8.1|`w-UdjPr-c`|[urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_1_s/external_oscillator_x/%2B4m608000_hz/%2B%2B28k8_baud/uart0_rxd0_txd1/led%2Bc7_csb3_dual/urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led%2Bc7_csb3_dual_pr_ce.hex)|
|510|512|u8.1|`we-djPr-c`|[urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_1_s/external_oscillator_x/%2B4m608000_hz/%2B%2B28k8_baud/uart0_rxd0_txd1/led%2Bc7_csb3_dual/urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led%2Bc7_csb3_dual_pr_ee_ce.hex)|
|512|512|u8.1|`weUdjPr--`|[urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_1_s/external_oscillator_x/%2B4m608000_hz/%2B%2B28k8_baud/uart0_rxd0_txd1/led%2Bc7_csb3_dual/urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led%2Bc7_csb3_dual_pr_ee.hex)|
|556|1024|u8.1|`weUdhpr-c`|[urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led+c7_csb3_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_1_s/external_oscillator_x/%2B4m608000_hz/%2B%2B28k8_baud/uart0_rxd0_txd1/led%2Bc7_csb3_dual/urboot_m1284p_1s_x4m608_28k8_uart0_rxd0_txd1_led%2Bc7_csb3_dual_ee_ce_hw.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `x4m608` is F<sub>CPU</sub> of an external oscillator, here 4.608 MHz
  + `28k8` shows the fixed communication baud rate, here 28800 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+c7` toggles an active-high (`+`) LED on pin `C7`
  + `csb3` uses pin B3 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1284p WDTO=1S F_CPU=20000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual
make MCU=atmega1284p WDTO=1S F_CPU=20000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr
make MCU=atmega1284p WDTO=1S F_CPU=20000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ce
make MCU=atmega1284p WDTO=1S F_CPU=20000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ee_ce
make MCU=atmega1284p WDTO=1S F_CPU=20000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ee
make MCU=atmega1284p WDTO=1S F_CPU=20000000L BAUD_RATE=125000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPC7 SFMCS=AtmelPB3 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfaa -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=64 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfaa -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=46 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=9 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=5 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=9 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcee0 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=468 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=20000000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=125000 -DLED=AtmelPC7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPB3 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_x20m0_125k0_uart0_rxd0_txd1_led+c7_csb3_dual_ee_ce_hw.elf urboot.c
```

