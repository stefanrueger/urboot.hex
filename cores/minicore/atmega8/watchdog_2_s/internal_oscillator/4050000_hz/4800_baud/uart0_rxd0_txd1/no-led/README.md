The ATmega8 exhibits a UART baud rate quantisation error of -0.50% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.50% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|234|256|u8.0|`w---jPr--`|[urboot_atmega8.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8.hex)|
|234|256|u8.0|`w---jPr--`|[urboot_atmega8_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8_pr.hex)|
|250|256|u8.0|`w---jPr-c`|[urboot_atmega8_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8_pr_ce.hex)|
|256|256|u8.0|`w-U-hpr--`|[urboot_atmega8_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8_hw.hex)|
|320|320|u8.0|`we--jPr-c`|[urboot_atmega8_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8_pr_ee_ce.hex)|
|320|320|u8.0|`weU-jPr--`|[urboot_atmega8_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8_pr_ee.hex)|
|368|512|u8.0|`weU-hpr-c`|[urboot_atmega8_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/minicore/atmega8/watchdog_2_s/internal_oscillator/4050000_hz/4800_baud/uart0_rxd0_txd1/no-led/urboot_atmega8_ee_ce_hw.hex)|

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
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr_ce
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_hw
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr_ee_ce
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr_ee
make MCU=atmega8 WDTO=2S F_CPU=8100000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=36 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=9 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcd -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf84 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=144 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega8 -DF_CPU=8100000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m8_2s_j8m0_9k6_uart0_rxd0_txd1_no-led_ee_ce_hw.elf urboot.c
```

