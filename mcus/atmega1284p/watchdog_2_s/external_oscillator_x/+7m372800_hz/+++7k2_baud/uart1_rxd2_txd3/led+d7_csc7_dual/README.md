The ATmega1284P exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|472|512|u8.1|`w-UdjPr--`|[urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led+d7_csc7_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B7k2_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led%2Bd7_csc7_dual.hex)|
|472|512|u8.1|`w-UdjPr--`|[urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led+d7_csc7_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B7k2_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led%2Bd7_csc7_dual_pr.hex)|
|504|512|u8.1|`w-UdjPr-c`|[urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B7k2_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led%2Bd7_csc7_dual_pr_ce.hex)|
|508|512|u8.1|`we-djPr-c`|[urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B7k2_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led%2Bd7_csc7_dual_pr_ee_ce.hex)|
|508|512|u8.1|`weUdjPr--`|[urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B7k2_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led%2Bd7_csc7_dual_pr_ee.hex)|
|562|1024|u8.1|`weUdhpr-c`|[urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega1284p/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B%2B%2B7k2_baud/uart1_rxd2_txd3/led%2Bd7_csc7_dual/urboot_m1284p_2s_x7m3728_7k2_uart1_rxd2_txd3_led%2Bd7_csc7_dual_ee_ce_hw.hex)|

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
  + `x7m3728` is F<sub>CPU</sub> of an external oscillator, here 7.3728 MHz
  + `7k2` shows the fixed communication baud rate, here 7200 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+d7` toggles an active-high (`+`) LED on pin `D7`
  + `csc7` uses pin C7 as chip select of external SPI flash memory for dual boot
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1284p WDTO=2S F_CPU=14745600L BAUD_RATE=14400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual
make MCU=atmega1284p WDTO=2S F_CPU=14745600L BAUD_RATE=14400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr
make MCU=atmega1284p WDTO=2S F_CPU=14745600L BAUD_RATE=14400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ce
make MCU=atmega1284p WDTO=2S F_CPU=14745600L BAUD_RATE=14400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ee_ce
make MCU=atmega1284p WDTO=2S F_CPU=14745600L BAUD_RATE=14400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ee
make MCU=atmega1284p WDTO=2S F_CPU=14745600L BAUD_RATE=14400 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPD7 SFMCS=AtmelPC7 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfad -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=40 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=8 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=8 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcee3 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=462 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=14400 -DLED=AtmelPD7 -DBLINK=1 -DDUAL=1 -DSFMCS=AtmelPC7 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_2s_x14m7456_14k4_uart1_rxd2_txd3_led+d7_csc7_dual_ee_ce_hw.elf urboot.c
```

